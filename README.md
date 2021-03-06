NativeJoystick
==============

AIR Native Extension (ANE) to support joysticks natively on the Windows platform.
It includes FlashDevelop project to build the demo, Visual Studio 2013 Express for Desktop C++ project to build the native DLL and batch files to build the extension into an ANE.

Copyright (C) 2014 Martin Sebastian Wain. All Rights Reserved.
http://2bam.com

Structure
=========
`/` - is the demo. NativeJoystickDemo.as3proj is the FlashDevelop project to run the AIR demo for Windows.

`/extension` - Everything needed to build the ANE (call BuildANE.bat)

`/extension/ane` - is the ANE itself in case you want to just grab it

`/extension/native/win32` - Everything needed to build the Windows DLL

How to build the ANE or demo
============================

1. Open `/extension/native/win32/NativeJoystickDLL.sln`
Build the solution in **Release** mode.

2. Edit `/bat/SetupSDK.bat` such that `FLEX_SDK` points to the correct Flex SDK folder in your drive.

3. Edit `/extension/unzip.bat` to run your favourite command-line usable unzipping program. It must decompress file `%1` to folder `%2`

4. Execute `/extension/BuildANE.bat` (sometimes takes it's time!)
		*-or-*
   Open `/NativeJoystickDemo.as3proj` and build/run which builds the ANE automatically on each run (unless you edit `/Run.bat`)

How to use the ANE in your own FlashDevelop project
===================================================
You must download the `/extension/ane/NativeJoystick.ane` (it's actually a ZIP file) and keep an unzipped directory of the same name for debugging.
You must additionally modify two `.bat` files that FlashDevelop generates for AIR projects.

This is done in order to use the zipped NativeJoystick.ane when packaging the app for deployment and the unzipped same-name folder while debugging. Don't ask me why, that's how it works.

You can use the same directories as the demo `/extension/ane` and `/extension/ane_unzipped`, or use the demo as guide.

1. Copy the `/extension/ane/*` and `/extension/ane_unzipped/*` folders to your project's folder

2. Edit /Run.bat (generated by FlashDevelop) and add `-extdir extension\ane_unzipped` to the end of the `adl` command
	It should read something like:
	`adl "%APP_XML%" "%APP_DIR%" -extdir extension\ane_unzipped`
	This will allow the ane to work/debug before packing the AIR application.
	
3. Edit /bat/Packager.bat (generated by FlashDevelop) and add `-extdir extension\ane` to the end of the `adt` command:
	`call adt -package %OPTIONS% %SIGNING_OPTIONS% %OUTPUT% %APP_XML% %FILE_OR_DIR% -extdir extension\ane`

4. Right click on the NativeJoystick.ane file at your FlashDevelop's Project window and click "Add To Library"

5. Go to Project->AIR App Properties and add the `com.iam2bam.ane.nativejoystick` text to the extension tab's list.

Tutorial on builing an ANE from scratch, step by step with screenshots is coming soon!

License
=======

All source code is licensed under the Mozilla Public License v2.0 (see LICENSE.MPL.txt or http://mozilla.org/MPL/2.0/)
with the exception of files `JoyOEMInfo.cpp` and `JoyOEMInfo.h` which are licensed under the MIT license
(license text included inside those files) which uses code from *FreeGlut* by *John F. Fay*
and `FlashRuntimeExtensions.h` which is copyright of *Adobe Systems Inc*.

All graphics (svg an png) copyright are dedicated to the Public Domain by a CC-0 license (http://creativecommons.org/publicdomain/zero/1.0/)
