{\rtf1\ansi\ansicpg1252\cocoartf2758
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fnil\fcharset0 Menlo-Bold;\f1\fnil\fcharset0 Menlo-Regular;}
{\colortbl;\red255\green255\blue255;\red252\green95\blue163;\red31\green31\blue36;\red255\green255\blue255;
\red93\green216\blue255;\red208\green168\blue255;\red208\green168\blue255;\red65\green161\blue192;\red161\green103\blue230;
\red158\green241\blue221;\red158\green241\blue221;\red103\green183\blue164;\red108\green121\blue134;\red161\green103\blue230;
\red208\green191\blue105;\red252\green106\blue93;\red103\green183\blue164;}
{\*\expandedcolortbl;;\csgenericrgb\c98839\c37355\c63833;\csgenericrgb\c12054\c12284\c14131;\csgenericrgb\c100000\c100000\c100000\c85000;
\csgenericrgb\c36295\c84643\c99897;\csgenericrgb\c81569\c65882\c100000;\csgenericrgb\c81681\c65692\c99927;\csgenericrgb\c25490\c63137\c75294;\csgenericrgb\c63232\c40219\c90115;
\csgenericrgb\c61961\c94510\c86667;\csgenericrgb\c62145\c94386\c86819;\csgenericrgb\c40538\c71705\c64209;\csgenericrgb\c42394\c47462\c52518;\csgenericrgb\c63137\c40392\c90196;
\csgenericrgb\c81498\c74939\c41233;\csgenericrgb\c98912\c41558\c36568;\csgenericrgb\c40392\c71765\c64314;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\deftab593
\pard\tx593\pardeftab593\partightenfactor0

\f0\b\fs24 \cf2 \cb3 import
\f1\b0 \cf4 \cb3  SwiftUI\

\f0\b \cf2 \cb3 import
\f1\b0 \cf4 \cb3  UIKit\

\f0\b \cf2 \cb3 import
\f1\b0 \cf4 \cb3  Foundation\

\f0\b \cf2 \cb3 import
\f1\b0 \cf4 \cb3  GoogleAPIClientForREST_Vision\
\

\f0\b \cf2 \cb3 struct
\f1\b0 \cf4 \cb3  \cf5 \cb3 ImagePicker\cf4 \cb3 : \cf6 \cb3 UIViewControllerRepresentable\cf4 \cb3  \{\
    \cf7 \cb3 @Binding\cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 selectedImage\cf4 \cb3 : \cf6 \cb3 UIImage\cf4 \cb3 ?\
    \cf7 \cb3 @Environment\cf4 \cb3 (\\.\cf9 \cb3 presentationMode\cf4 \cb3 ) 
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 presentationMode\cf4 \cb3 \
    
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 onImagePicked\cf4 \cb3 : (\cf6 \cb3 UIImage\cf4 \cb3 ) -> \cf7 \cb3 Void\cf4 \cb3 \
    
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 onSearchForTires\cf4 \cb3 : () -> \cf7 \cb3 Void\cf4 \cb3 \
        \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 makeCoordinator\cf4 \cb3 () -> \cf10 \cb3 Coordinator\cf4 \cb3  \{\
        \cf10 \cb3 Coordinator\cf4 \cb3 (
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 )\
    \}\
        \
    
\f0\b \cf2 \cb3 class
\f1\b0 \cf4 \cb3  \cf5 \cb3 Coordinator\cf4 \cb3 : \cf6 \cb3 NSObject\cf4 \cb3 , \cf6 \cb3 UINavigationControllerDelegate\cf4 \cb3 , \cf6 \cb3 UIImagePickerControllerDelegate\cf4 \cb3  \{\
        
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 parent\cf4 \cb3 : \cf11 \cb3 ImagePicker\cf4 \cb3 \
            \
        
\f0\b \cf2 \cb3 init
\f1\b0 \cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  parent: \cf11 \cb3 ImagePicker\cf4 \cb3 ) \{\
            
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 parent\cf4 \cb3  = parent\
        \}\
            \
        
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 imagePickerController\cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  picker: \cf6 \cb3 UIImagePickerController\cf4 \cb3 , \cf8 \cb3 didFinishPickingMediaWithInfo\cf4 \cb3  info: [\cf6 \cb3 UIImagePickerController\cf4 \cb3 .\cf7 \cb3 InfoKey\cf4 \cb3  : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ]) \{\
            
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  image = info[.\cf9 \cb3 originalImage\cf4 \cb3 ] 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? \cf6 \cb3 UIImage\cf4 \cb3  \{\
                \cf12 \cb3 parent\cf4 \cb3 .\cf12 \cb3 selectedImage\cf4 \cb3  = image\
                \cf12 \cb3 parent\cf4 \cb3 .onImagePicked(image)\
            \}\
            \cf12 \cb3 parent\cf4 \cb3 .\cf12 \cb3 presentationMode\cf4 \cb3 .\cf9 \cb3 wrappedValue\cf4 \cb3 .dismiss()\
        \}\
            \
        
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 imagePickerControllerDidCancel\cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  picker: \cf6 \cb3 UIImagePickerController\cf4 \cb3 ) \{\
            \cf12 \cb3 parent\cf4 \cb3 .\cf12 \cb3 presentationMode\cf4 \cb3 .\cf9 \cb3 wrappedValue\cf4 \cb3 .dismiss()\
        \}\
            \
    \}\
        \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 makeUIViewController\cf4 \cb3 (\cf8 \cb3 context\cf4 \cb3 : \cf7 \cb3 UIViewControllerRepresentableContext\cf4 \cb3 <\cf11 \cb3 ImagePicker\cf4 \cb3 >) -> \cf6 \cb3 UIImagePickerController\cf4 \cb3  \{\
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  imagePicker = \cf6 \cb3 UIImagePickerController\cf4 \cb3 ()\
        imagePicker.\cf9 \cb3 sourceType\cf4 \cb3  = .\cf9 \cb3 camera\cf4 \cb3 \
        imagePicker.\cf9 \cb3 delegate\cf4 \cb3  = context.\cf9 \cb3 coordinator\cf4 \cb3 \
        
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3  imagePicker\
    \}\
        \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 updateUIViewController\cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  uiViewController: \cf6 \cb3 UIImagePickerController\cf4 \cb3 , \cf8 \cb3 context\cf4 \cb3 : \cf7 \cb3 UIViewControllerRepresentableContext\cf4 \cb3 <\cf11 \cb3 ImagePicker\cf4 \cb3 >) \{\
            \cf13 \cb3 // Nothing to do here\cf4 \cb3 \
    \}\
\}\
\

\f0\b \cf2 \cb3 class
\f1\b0 \cf4 \cb3  \cf5 \cb3 Coordinator\cf4 \cb3 : \cf6 \cb3 NSObject\cf4 \cb3 , \cf6 \cb3 UINavigationControllerDelegate\cf4 \cb3 , \cf6 \cb3 UIImagePickerControllerDelegate\cf4 \cb3  \{\
    
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 parent\cf4 \cb3 : \cf11 \cb3 ImagePicker\cf4 \cb3 \
    \
    
\f0\b \cf2 \cb3 init
\f1\b0 \cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  parent: \cf11 \cb3 ImagePicker\cf4 \cb3 ) \{\
        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 parent\cf4 \cb3  = parent\
    \}\
    \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 imagePickerController\cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  picker: \cf6 \cb3 UIImagePickerController\cf4 \cb3 , \cf8 \cb3 didFinishPickingMediaWithInfo\cf4 \cb3  info: [\cf6 \cb3 UIImagePickerController\cf4 \cb3 .\cf7 \cb3 InfoKey\cf4 \cb3  : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ]) \{\
        
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  image = info[.\cf9 \cb3 originalImage\cf4 \cb3 ] 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? \cf6 \cb3 UIImage\cf4 \cb3  \{\
            \cf12 \cb3 parent\cf4 \cb3 .\cf12 \cb3 selectedImage\cf4 \cb3  = image\
            \cf12 \cb3 parent\cf4 \cb3 .onImagePicked(image)\
            \cf12 \cb3 parent\cf4 \cb3 .onSearchForTires() \cf13 \cb3 // Call the closure here\cf4 \cb3 \
        \}\
        \cf12 \cb3 parent\cf4 \cb3 .\cf12 \cb3 presentationMode\cf4 \cb3 .\cf9 \cb3 wrappedValue\cf4 \cb3 .dismiss()\
    \}\
\}\
\

\f0\b \cf2 \cb3 extension
\f1\b0 \cf4 \cb3  \cf5 \cb3 Color\cf4 \cb3  \{\
    
\f0\b \cf2 \cb3 init
\f1\b0 \cf4 \cb3 (\cf8 \cb3 hex\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3 ) \{\
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  hex = hex.\cf14 \cb3 trimmingCharacters\cf4 \cb3 (\cf14 \cb3 in\cf4 \cb3 : \cf7 \cb3 CharacterSet\cf4 \cb3 .\cf9 \cb3 alphanumerics\cf4 \cb3 .\cf9 \cb3 inverted\cf4 \cb3 )\
        
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  int: \cf7 \cb3 UInt64\cf4 \cb3  = \cf15 \cb3 0\cf4 \cb3 \
        \cf6 \cb3 Scanner\cf4 \cb3 (\cf14 \cb3 string\cf4 \cb3 : hex).\cf14 \cb3 scanHexInt64\cf4 \cb3 (&int)\
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  a, r, g, b: \cf7 \cb3 UInt64\cf4 \cb3 \
        
\f0\b \cf2 \cb3 switch
\f1\b0 \cf4 \cb3  hex.\cf9 \cb3 count\cf4 \cb3  \{\
        
\f0\b \cf2 \cb3 case
\f1\b0 \cf4 \cb3  \cf15 \cb3 3\cf4 \cb3 : \cf13 \cb3 // RGB (12-bit)\cf4 \cb3 \
            (a, r, g, b) = (\cf15 \cb3 255\cf4 \cb3 , (int >> \cf15 \cb3 8\cf4 \cb3 ) * \cf15 \cb3 17\cf4 \cb3 , (int >> \cf15 \cb3 4\cf4 \cb3  & \cf15 \cb3 0xF\cf4 \cb3 ) * \cf15 \cb3 17\cf4 \cb3 , (int & \cf15 \cb3 0xF\cf4 \cb3 ) * \cf15 \cb3 17\cf4 \cb3 )\
        
\f0\b \cf2 \cb3 case
\f1\b0 \cf4 \cb3  \cf15 \cb3 6\cf4 \cb3 : \cf13 \cb3 // RGB (24-bit)\cf4 \cb3 \
            (a, r, g, b) = (\cf15 \cb3 255\cf4 \cb3 , int >> \cf15 \cb3 16\cf4 \cb3 , int >> \cf15 \cb3 8\cf4 \cb3  & \cf15 \cb3 0xFF\cf4 \cb3 , int & \cf15 \cb3 0xFF\cf4 \cb3 )\
        
\f0\b \cf2 \cb3 case
\f1\b0 \cf4 \cb3  \cf15 \cb3 8\cf4 \cb3 : \cf13 \cb3 // ARGB (32-bit)\cf4 \cb3 \
            (a, r, g, b) = (int >> \cf15 \cb3 24\cf4 \cb3 , int >> \cf15 \cb3 16\cf4 \cb3  & \cf15 \cb3 0xFF\cf4 \cb3 , int >> \cf15 \cb3 8\cf4 \cb3  & \cf15 \cb3 0xFF\cf4 \cb3 , int & \cf15 \cb3 0xFF\cf4 \cb3 )\
        
\f0\b \cf2 \cb3 default
\f1\b0 \cf4 \cb3 :\
            (a, r, g, b) = (\cf15 \cb3 255\cf4 \cb3 , \cf15 \cb3 0\cf4 \cb3 , \cf15 \cb3 0\cf4 \cb3 , \cf15 \cb3 0\cf4 \cb3 )\
        \}\
        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf14 \cb3 init\cf4 \cb3 (\
            .\cf9 \cb3 sRGB\cf4 \cb3 ,\
            \cf14 \cb3 red\cf4 \cb3 : \cf7 \cb3 Double\cf4 \cb3 (r) / \cf15 \cb3 255\cf4 \cb3 ,\
            \cf14 \cb3 green\cf4 \cb3 : \cf7 \cb3 Double\cf4 \cb3 (g) / \cf15 \cb3 255\cf4 \cb3 ,\
            \cf14 \cb3 blue\cf4 \cb3 :  \cf7 \cb3 Double\cf4 \cb3 (b) / \cf15 \cb3 255\cf4 \cb3 ,\
            \cf14 \cb3 opacity\cf4 \cb3 : \cf7 \cb3 Double\cf4 \cb3 (a) / \cf15 \cb3 255\cf4 \cb3 \
        )\
    \}\
\}\
\

\f0\b \cf2 \cb3 struct
\f1\b0 \cf4 \cb3  \cf5 \cb3 ContentView\cf4 \cb3 : \cf6 \cb3 View\cf4 \cb3  \{\
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 isShowingImagePicker\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 selectedImage\cf4 \cb3 : \cf6 \cb3 UIImage\cf4 \cb3 ?\
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 tireSize\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3  = \cf16 \cb3 ""\cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 tireRatio\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3  = \cf16 \cb3 ""\cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 tireRadius\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3  = \cf16 \cb3 ""\cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 apiResult\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3  = \cf16 \cb3 ""\cf4 \cb3  \cf13 \cb3 // Store the API result here\cf4 \cb3 \
    \cf7 \cb3 @State\cf4 \cb3  
\f0\b \cf2 \cb3 private
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3 \
    \
    \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 searchForTires\cf4 \cb3 (\cf8 \cb3 size\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3 , \cf8 \cb3 ratio\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3 , \cf8 \cb3 radius\cf4 \cb3 : \cf7 \cb3 String\cf4 \cb3 ) \{\
        \cf13 \cb3 // Implement your tire searching logic here\cf4 \cb3 \
        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = \cf16 \cb3 "Searched for tires with size: \cf4 \cb3 \\(size)\cf16 \cb3 , ratio: \cf4 \cb3 \\(ratio)\cf16 \cb3 , radius: \cf4 \cb3 \\(radius)\cf16 \cb3 "\cf4 \cb3 \
        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
    \}\
    \
    
\f0\b \cf2 \cb3 func
\f1\b0 \cf4 \cb3  \cf8 \cb3 processImageForTextRecognition\cf4 \cb3 (\cf8 \cb3 _\cf4 \cb3  image: \cf6 \cb3 UIImage\cf4 \cb3 ) \{\
        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3  \cf13 \cb3 // Start loading\cf4 \cb3 \
        \cf13 \cb3 // Convert image to base64 string\cf4 \cb3 \
        
\f0\b \cf2 \cb3 guard
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  imageData = image.jpegData(compressionQuality: \cf15 \cb3 0.8\cf4 \cb3 ) 
\f0\b \cf2 \cb3 else
\f1\b0 \cf4 \cb3  \{\
            
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3  \cf13 \cb3 // Stop loading indicator in case of error\cf4 \cb3 \
            
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3 \
        \}\
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  base64EncodedImage = imageData.\cf14 \cb3 base64EncodedString\cf4 \cb3 (\cf14 \cb3 options\cf4 \cb3 : .\cf9 \cb3 endLineWithCarriageReturn\cf4 \cb3 )\
        \
        \cf13 \cb3 // Construct the API request\cf4 \cb3 \
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  jsonRequest: [\cf7 \cb3 String\cf4 \cb3 : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ] = [\
            \cf16 \cb3 "requests"\cf4 \cb3 : [\
                \cf16 \cb3 "image"\cf4 \cb3 : [\cf16 \cb3 "content"\cf4 \cb3 : base64EncodedImage],\
                \cf16 \cb3 "features"\cf4 \cb3 : [[\cf16 \cb3 "type"\cf4 \cb3 : \cf16 \cb3 "TEXT_DETECTION"\cf4 \cb3 ]]\
            ]\
        ]\
        \
        \cf13 \cb3 // Convert request to JSON data\cf4 \cb3 \
        
\f0\b \cf2 \cb3 guard
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  jsonData = 
\f0\b \cf2 \cb3 try
\f1\b0 \cf4 \cb3 ? \cf6 \cb3 JSONSerialization\cf4 \cb3 .\cf14 \cb3 data\cf4 \cb3 (\cf14 \cb3 withJSONObject\cf4 \cb3 : jsonRequest, \cf14 \cb3 options\cf4 \cb3 : []) 
\f0\b \cf2 \cb3 else
\f1\b0 \cf4 \cb3  \{\
            
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3  \cf13 \cb3 // Stop loading indicator in case of error\cf4 \cb3 \
            
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3 \
        \}\
        \
        \cf13 \cb3 // Set up the URL and URLRequest\cf4 \cb3 \
        
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  urlString = \cf16 \cb3 "https://vision.googleapis.com/v1/images:annotate?key=AIzaSyBVDbEs6SizW7n4R0RM76l-QpbE8pgWp1c"\cf4 \cb3 \
        
\f0\b \cf2 \cb3 guard
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  url = \cf7 \cb3 URL\cf4 \cb3 (\cf14 \cb3 string\cf4 \cb3 : urlString) 
\f0\b \cf2 \cb3 else
\f1\b0 \cf4 \cb3  \{ 
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3  \}\
        
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  request = \cf7 \cb3 URLRequest\cf4 \cb3 (\cf14 \cb3 url\cf4 \cb3 : url)\
        request.\cf9 \cb3 httpMethod\cf4 \cb3  = \cf16 \cb3 "POST"\cf4 \cb3 \
        request.\cf9 \cb3 httpBody\cf4 \cb3  = jsonData\
        request.\cf14 \cb3 addValue\cf4 \cb3 (\cf16 \cb3 "application/json"\cf4 \cb3 , \cf14 \cb3 forHTTPHeaderField\cf4 \cb3 : \cf16 \cb3 "Content-Type"\cf4 \cb3 )\
        \
        \cf13 \cb3 // Perform the API request\cf4 \cb3 \
        \cf6 \cb3 URLSession\cf4 \cb3 .\cf9 \cb3 shared\cf4 \cb3 .\cf14 \cb3 dataTask\cf4 \cb3 (\cf14 \cb3 with\cf4 \cb3 : request) \{ data, response, error 
\f0\b \cf2 \cb3 in
\f1\b0 \cf4 \cb3 \
            DispatchQueue.\cf9 \cb3 main\cf4 \cb3 .\cf14 \cb3 async\cf4 \cb3  \{\
                
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 false
\f1\b0 \cf4 \cb3  \cf13 \cb3 // Trigger navigation to ResultsView\cf4 \cb3 \
            \}\
            \
            
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  error = error \{\
                DispatchQueue.\cf9 \cb3 main\cf4 \cb3 .\cf14 \cb3 async\cf4 \cb3  \{\
                    \cf14 \cb3 print\cf4 \cb3 (\cf16 \cb3 "Network request error: \cf4 \cb3 \\(error.\cf9 \cb3 localizedDescription\cf4 \cb3 )\cf16 \cb3 "\cf4 \cb3 )\
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = \cf16 \cb3 "Error: \cf4 \cb3 \\(error.\cf9 \cb3 localizedDescription\cf4 \cb3 )\cf16 \cb3 "\cf4 \cb3 \
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                \}\
                
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3 \
            \}\
            \
            
\f0\b \cf2 \cb3 guard
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  data = data 
\f0\b \cf2 \cb3 else
\f1\b0 \cf4 \cb3  \{\
                DispatchQueue.\cf9 \cb3 main\cf4 \cb3 .\cf14 \cb3 async\cf4 \cb3  \{\
                    \cf14 \cb3 print\cf4 \cb3 (\cf16 \cb3 "No data received from the API"\cf4 \cb3 )\
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = \cf16 \cb3 "Error: Data not found"\cf4 \cb3 \
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                \}\
                
\f0\b \cf2 \cb3 return
\f1\b0 \cf4 \cb3 \
            \}\
            \
            \cf13 \cb3 // Parse the response\cf4 \cb3 \
            
\f0\b \cf2 \cb3 do
\f1\b0 \cf4 \cb3  \{\
                
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  jsonResponse = 
\f0\b \cf2 \cb3 try
\f1\b0 \cf4 \cb3  \cf6 \cb3 JSONSerialization\cf4 \cb3 .\cf14 \cb3 jsonObject\cf4 \cb3 (\cf14 \cb3 with\cf4 \cb3 : data, \cf14 \cb3 options\cf4 \cb3 : []) 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? [\cf7 \cb3 String\cf4 \cb3 : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ],\
                   
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  responses = jsonResponse[\cf16 \cb3 "responses"\cf4 \cb3 ] 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? [[\cf7 \cb3 String\cf4 \cb3 : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ]],\
                   
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  response = responses.\cf9 \cb3 first\cf4 \cb3 ,\
                   
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  textAnnotations = response[\cf16 \cb3 "textAnnotations"\cf4 \cb3 ] 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? [[\cf7 \cb3 String\cf4 \cb3 : 
\f0\b \cf2 \cb3 Any
\f1\b0 \cf4 \cb3 ]],\
                   
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  firstAnnotation = textAnnotations.\cf9 \cb3 first\cf4 \cb3 ,\
                   
\f0\b \cf2 \cb3 let
\f1\b0 \cf4 \cb3  detectedText = firstAnnotation[\cf16 \cb3 "description"\cf4 \cb3 ] 
\f0\b \cf2 \cb3 as
\f1\b0 \cf4 \cb3 ? \cf7 \cb3 String\cf4 \cb3  \{\
                    \
                    DispatchQueue.\cf9 \cb3 main\cf4 \cb3 .\cf14 \cb3 async\cf4 \cb3  \{\
                        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = detectedText\
                        
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3  \cf13 \cb3 // Trigger navigation to ResultsView\cf4 \cb3 \
                    \}\
                \}\
            \} 
\f0\b \cf2 \cb3 catch
\f1\b0 \cf4 \cb3  \{\
                DispatchQueue.\cf9 \cb3 main\cf4 \cb3 .\cf14 \cb3 async\cf4 \cb3  \{\
                    \cf14 \cb3 print\cf4 \cb3 (\cf16 \cb3 "JSON Parsing Error: \cf4 \cb3 \\(error.\cf9 \cb3 localizedDescription\cf4 \cb3 )\cf16 \cb3 "\cf4 \cb3 )\
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = \cf16 \cb3 "Error: \cf4 \cb3 \\(error.\cf9 \cb3 localizedDescription\cf4 \cb3 )\cf16 \cb3 "\cf4 \cb3 \
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                \}\
            \}\
            \
            \cf13 \cb3 // Handle the API response...\cf4 \cb3 \
            \cf13 \cb3 // Update your UI accordingly...\cf4 \cb3 \
        \}.\cf14 \cb3 resume\cf4 \cb3 ()\
    \}\
    \
    
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 body\cf4 \cb3 : 
\f0\b \cf2 \cb3 some
\f1\b0 \cf4 \cb3  \cf6 \cb3 View\cf4 \cb3  \{\
        \cf7 \cb3 NavigationStack\cf4 \cb3  \{\
            \cf7 \cb3 GeometryReader\cf4 \cb3  \{ geo 
\f0\b \cf2 \cb3 in
\f1\b0 \cf4 \cb3 \
                \cf7 \cb3 ZStack\cf4 \cb3 \{\
                    \cf7 \cb3 Image\cf4 \cb3 (\cf16 \cb3 "Mainbg"\cf4 \cb3 )\
                        .\cf14 \cb3 resizable\cf4 \cb3 ()\
                        .\cf14 \cb3 scaledToFill\cf4 \cb3 ()\
                        .\cf14 \cb3 edgesIgnoringSafeArea\cf4 \cb3 (.\cf9 \cb3 all\cf4 \cb3 )\
                        .\cf14 \cb3 frame\cf4 \cb3 (\cf14 \cb3 width\cf4 \cb3 :  geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 width\cf4 \cb3 , \cf14 \cb3 height\cf4 \cb3 : geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 height\cf4 \cb3 , \cf14 \cb3 alignment\cf4 \cb3 : \cf7 \cb3 Alignment\cf4 \cb3 (\cf14 \cb3 horizontal\cf4 \cb3 : .\cf9 \cb3 trailing\cf4 \cb3 , \cf14 \cb3 vertical\cf4 \cb3 : .\cf9 \cb3 center\cf4 \cb3 ))\
                        . \cf14 \cb3 opacity\cf4 \cb3 (\cf15 \cb3 1.0\cf4 \cb3 )\
                    
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  \cf12 \cb3 isLoading\cf4 \cb3  \{\
                        \cf7 \cb3 ProgressView\cf4 \cb3 (\cf16 \cb3 "Sending image..."\cf4 \cb3 )\
                            .\cf14 \cb3 progressViewStyle\cf4 \cb3 (\cf7 \cb3 CircularProgressViewStyle\cf4 \cb3 ())\
                    \} 
\f0\b \cf2 \cb3 else
\f1\b0 \cf4 \cb3  \{\
                        \
                        \cf7 \cb3 VStack\cf4 \cb3  \{\
                            \cf7 \cb3 Spacer\cf4 \cb3 ()\
                                .\cf14 \cb3 frame\cf4 \cb3 (\cf14 \cb3 height\cf4 \cb3 : geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 height\cf4 \cb3  * \cf15 \cb3 0.045\cf4 \cb3 ) \cf13 \cb3 // Adjust this value to move the text up or down\cf4 \cb3 \
                            \
                            \cf7 \cb3 Text\cf4 \cb3 (\cf16 \cb3 "TireScan AI"\cf4 \cb3 )\
                                .\cf14 \cb3 font\cf4 \cb3 (.\cf14 \cb3 system\cf4 \cb3 (\cf14 \cb3 size\cf4 \cb3 : \cf15 \cb3 60\cf4 \cb3 ))\
                                .\cf14 \cb3 fontWeight\cf4 \cb3 (.\cf9 \cb3 bold\cf4 \cb3 )\
                                .\cf14 \cb3 foregroundColor\cf4 \cb3 (.\cf9 \cb3 white\cf4 \cb3 )\
                                .\cf14 \cb3 multilineTextAlignment\cf4 \cb3 (.\cf9 \cb3 center\cf4 \cb3 )\
                            \
                            \cf7 \cb3 Spacer\cf4 \cb3 ()\
                                .\cf14 \cb3 frame\cf4 \cb3 (\cf14 \cb3 height\cf4 \cb3 : geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 height\cf4 \cb3  * \cf15 \cb3 0.055\cf4 \cb3 ) \cf13 \cb3 // Adjust this value to move the text up or down\cf4 \cb3 \
                            \
                            \cf7 \cb3 Text\cf4 \cb3 (\cf16 \cb3 "By Diep Nguyen"\cf4 \cb3 )\
                                .\cf14 \cb3 lineLimit\cf4 \cb3 (\cf15 \cb3 1\cf4 \cb3 )\
                                .\cf14 \cb3 font\cf4 \cb3 (.\cf14 \cb3 system\cf4 \cb3 (\cf14 \cb3 size\cf4 \cb3 : \cf15 \cb3 20\cf4 \cb3 ))\
                                .\cf14 \cb3 fontWeight\cf4 \cb3 (.\cf9 \cb3 bold\cf4 \cb3 )\
                                .\cf14 \cb3 foregroundColor\cf4 \cb3 (.\cf9 \cb3 white\cf4 \cb3 )\
                                .\cf14 \cb3 multilineTextAlignment\cf4 \cb3 (.\cf9 \cb3 center\cf4 \cb3 )\
                                .\cf14 \cb3 background\cf4 \cb3 (\cf7 \cb3 Color\cf4 \cb3 (\cf17 \cb3 hex\cf4 \cb3 : \cf16 \cb3 "14354A"\cf4 \cb3 ))\
                                .\cf14 \cb3 cornerRadius\cf4 \cb3 (\cf15 \cb3 50\cf4 \cb3 )\
                            \
                            \cf7 \cb3 Text\cf4 \cb3 (\cf16 \cb3 "Harvard CS50 Final Project"\cf4 \cb3 )\
                                .\cf14 \cb3 lineLimit\cf4 \cb3 (\cf15 \cb3 1\cf4 \cb3 )\
                                .\cf14 \cb3 font\cf4 \cb3 (.\cf14 \cb3 system\cf4 \cb3 (\cf14 \cb3 size\cf4 \cb3 : \cf15 \cb3 13\cf4 \cb3 ))\
                                .\cf14 \cb3 fontWeight\cf4 \cb3 (.\cf9 \cb3 bold\cf4 \cb3 )\
                                .\cf14 \cb3 foregroundColor\cf4 \cb3 (.\cf9 \cb3 white\cf4 \cb3 )\
                                .\cf14 \cb3 multilineTextAlignment\cf4 \cb3 (.\cf9 \cb3 center\cf4 \cb3 )\
                                .\cf14 \cb3 background\cf4 \cb3 (\cf7 \cb3 Color\cf4 \cb3 (\cf17 \cb3 hex\cf4 \cb3 : \cf16 \cb3 "14354A"\cf4 \cb3 ))\
                                .\cf14 \cb3 cornerRadius\cf4 \cb3 (\cf15 \cb3 50\cf4 \cb3 )\
                            \
                            \cf7 \cb3 Spacer\cf4 \cb3 ()\
                                .\cf14 \cb3 frame\cf4 \cb3 (\cf14 \cb3 height\cf4 \cb3 : geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 height\cf4 \cb3  * \cf15 \cb3 0.47\cf4 \cb3 )\cf13 \cb3 // This spacer will push the button down. Adjust its size as needed.\cf4 \cb3 \
                            \
                            \cf7 \cb3 Button\cf4 \cb3 (\cf14 \cb3 action\cf4 \cb3 : \{\
                                
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isShowingImagePicker\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                            \}\
                            ) \{\
                                \cf7 \cb3 Text\cf4 \cb3 (\cf16 \cb3 "Press To Scan Tire"\cf4 \cb3 )\
                                    .\cf14 \cb3 font\cf4 \cb3 (.\cf9 \cb3 title\cf4 \cb3 )\
                                    .\cf14 \cb3 foregroundColor\cf4 \cb3 (.\cf9 \cb3 white\cf4 \cb3 )\
                                    .\cf14 \cb3 padding\cf4 \cb3 ()\
                                    .\cf14 \cb3 background\cf4 \cb3 (\cf7 \cb3 Color\cf4 \cb3 (\cf17 \cb3 hex\cf4 \cb3 : \cf16 \cb3 "14354A"\cf4 \cb3 ))\
                                    .\cf14 \cb3 cornerRadius\cf4 \cb3 (\cf15 \cb3 50\cf4 \cb3 )\
                            \}\
                            .\cf14 \cb3 frame\cf4 \cb3 (\cf14 \cb3 width\cf4 \cb3 : geo.\cf9 \cb3 size\cf4 \cb3 .\cf9 \cb3 width\cf4 \cb3  * \cf15 \cb3 0.8\cf4 \cb3 , \cf14 \cb3 height\cf4 \cb3 : \cf15 \cb3 80\cf4 \cb3 , \cf14 \cb3 alignment\cf4 \cb3 : .\cf9 \cb3 center\cf4 \cb3 ) \cf13 \cb3 // Adjust width and height as needed\cf4 \cb3 \
                            .\cf14 \cb3 sheet\cf4 \cb3 (\cf14 \cb3 isPresented\cf4 \cb3 : \cf12 \cb3 $isShowingImagePicker\cf4 \cb3 ) \{\
                                \cf11 \cb3 ImagePicker\cf4 \cb3 (\cf11 \cb3 selectedImage\cf4 \cb3 : \cf12 \cb3 $selectedImage\cf4 \cb3 ,\
                                            \cf11 \cb3 onImagePicked\cf4 \cb3 : \{ image 
\f0\b \cf2 \cb3 in
\f1\b0 \cf4 \cb3 \
                                                
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf17 \cb3 processImageForTextRecognition\cf4 \cb3 (image)\
                                \},\
                                \cf11 \cb3 onSearchForTires\cf4 \cb3 : \{\
                                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 isLoading\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                                \})\
                            \}\
                            \
                            \cf7 \cb3 Spacer\cf4 \cb3 () \cf13 \cb3 // You can adjust or remove this spacer based on how much space you want at the bottom\cf4 \cb3 \
                            
\f0\b \cf2 \cb3 if
\f1\b0 \cf4 \cb3  !\cf12 \cb3 tireSize\cf4 \cb3 .\cf9 \cb3 isEmpty\cf4 \cb3  && !\cf12 \cb3 tireRatio\cf4 \cb3 .\cf9 \cb3 isEmpty\cf4 \cb3  && !\cf12 \cb3 tireRadius\cf4 \cb3 .\cf9 \cb3 isEmpty\cf4 \cb3  \{\
                                \cf7 \cb3 Button\cf4 \cb3 (\cf16 \cb3 "Search for Tires"\cf4 \cb3 ) \{\
                                    \cf17 \cb3 searchForTires\cf4 \cb3 (\cf17 \cb3 size\cf4 \cb3 : \cf12 \cb3 tireSize\cf4 \cb3 , \cf17 \cb3 ratio\cf4 \cb3 : \cf12 \cb3 tireRatio\cf4 \cb3 , \cf17 \cb3 radius\cf4 \cb3 : \cf12 \cb3 tireRadius\cf4 \cb3 )\
                                \}\
                                .\cf14 \cb3 foregroundColor\cf4 \cb3 (.\cf9 \cb3 blue\cf4 \cb3 )\
                            \}\
                        \}\
                        \
                    \}\
                \}\
                \cf7 \cb3 Button\cf4 \cb3 (\cf16 \cb3 "Show Results"\cf4 \cb3 ) \{\
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 apiResult\cf4 \cb3  = \cf16 \cb3 "Test Result"\cf4 \cb3 \
                    
\f0\b \cf2 \cb3 self
\f1\b0 \cf4 \cb3 .\cf12 \cb3 showResultsView\cf4 \cb3  = 
\f0\b \cf2 \cb3 true
\f1\b0 \cf4 \cb3 \
                \}\
            \}\
            .\cf14 \cb3 navigationDestination\cf4 \cb3 (\cf14 \cb3 isPresented\cf4 \cb3 : \cf12 \cb3 $showResultsView\cf4 \cb3 ) \{\
                \cf13 \cb3 // Destination view when showResultsView is true\cf4 \cb3 \
                \cf11 \cb3 ResultsView\cf4 \cb3 (\cf17 \cb3 result\cf4 \cb3 : \cf12 \cb3 apiResult\cf4 \cb3 )\
            \}\
        \}\
\
    \}\
    \
\
    \}\
    \

\f0\b \cf2 \cb3 struct
\f1\b0 \cf4 \cb3  \cf5 \cb3 ContentView_Previews\cf4 \cb3 : \cf6 \cb3 PreviewProvider\cf4 \cb3  \{\
    
\f0\b \cf2 \cb3 static
\f1\b0 \cf4 \cb3  
\f0\b \cf2 \cb3 var
\f1\b0 \cf4 \cb3  \cf8 \cb3 previews\cf4 \cb3 : 
\f0\b \cf2 \cb3 some
\f1\b0 \cf4 \cb3  \cf6 \cb3 View\cf4 \cb3  \{\
        \cf11 \cb3 ContentView\cf4 \cb3 ()\
    \}\
\}\
}