cmake_minimum_required(VERSION 2.8.8)
project (sample)

include (../JsonParsing.cmake)

ParseJson (${PROJECT_SOURCE_DIR}/test.json ROOT jsonRoot)
isObject (${jsonRoot} isObject)
if (isObject)
   GetObjectElementName (${jsonRoot} rootName)
   message(STATUS "Name of the root is ${rootName}")
   GetObjectElement (${jsonRoot} rootElement) #Return path to root object (json has on object at the root normally)
   GetObjectElement (${rootElement} objectElement) #Get List of all element in the object 
   message(STATUS "objectElement : ${objectElement}") 
   foreach (el IN LISTS objectElement)
      isArray (${el} isAnArray) #Check each element to validate it's an Array
      if (isAnArray)
         GetArraySize(${el} size) #Tell User the size of the array (Starts at 0)
         GetArray (${el} array) #Get an array of element
		 math(EXPR size "${size}+1")
         message (STATUS "We have an array of ${size} elements")
		 foreach (el IN LISTS array)
			GetElement(${el} "servlet-name" namePath) #We want the element "servlet-name" in the object element of the array
			isValue(${namePath} isValue) #Validate that "servlet-name" is a value
			if (isValue)
				GetValue(${namePath} servetName) #if it is a value get it and print it
				message(STATUS "Servet-Name = ${servetName}")
			endif ()
		 endforeach ()
	  endif ()
   endforeach ()

   GetElement(${jsonRoot} "web-app.taglib.taglib-uri" taglibUriPath)
   isValue(${taglibUriPath} FoundTagUri)
   if (FoundTagUri)
      getValue(${taglibUriPath} TagUriValue)
	  message(STATUS "Taglib-uri is ${TagUriValue}")
   else ()
      message(ERROR " : Could not find Taglib-uri")
   endif ()
  
   GetElement(${jsonRoot} "web-app.servlet.4.servlet-name" servletNameClassPath)
   isValue(${servletNameClassPath} FoundservletName)
   if (FoundservletName)
      getValue(${servletNameClassPath} servletName)
	  message(STATUS "servlet-name of the 5 servet is ${servletName}")
   else ()
      message(ERROR " : Could not find servlet-name")
   endif ()
   
endif ()

