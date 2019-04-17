Instructions how to build the PyGTK-Installer for Inkscape 0.92.4

Note: Steps 1-3 (excl. compilation) are scripted now, see download-and-prepare bash script!

The remaining points needs to be scripted!!

1. Create a directory with the name "files" and two subdirectories mingw32 and mingw64

2. Create a directory with the name "build"

3. Populate the directory "files/mingw64" with the content of the MINGW-directories of the following 
   archives from http://repo.msys2.org/mingw/x86_64/ (for 64-bit installation):
      
	mingw-w64-x86_64-glib2-2.58.2-1-any.pkg.tar   
	mingw-w64-x86_64-gtksourceview2-2.10.5-3-any.pkg.tar
	mingw-w64-x86_64-python2-cairo-1.18.0-1-any.pkg.tar
	mingw-w64-x86_64-python2-gobject2-2.28.7-1.pkg.tar
	mingw-w64-x86_64-python2-pygtk-2.24.0-6-any.pkg.tar	
	mingw-w64-x86_64-pygtksourceview2
	
   and with the content of the MINGW-directories of the following 
   archives from http://repo.msys2.org/mingw/i686/ (for 32-bit installation):

	mingw-w64-i686-glib2-2.58.2-1-any.pkg.tar   
	mingw-w64-i686-gtksourceview2-2.10.5-3-any.pkg.tar
	mingw-w64-i686-python2-cairo-1.18.0-1-any.pkg.tar
	mingw-w64-i686-python2-gobject2-2.28.7-1.pkg.tar
	mingw-w64-i686-python2-pygtk-2.24.0-6-any.pkg.tar	
	mingw-w64-i686-pygtksourceview2-2.10.1

	
   After this operation the files directory should contain the directories mingw32 and mingw64 
   each of them containing four subdirectories: bin, inlcude, Lib, share

   If one or more of these packages are missing in the above link build them on your own using
   MINGW (you will have to do this at least with pygtksourceview). 
   Repository: 	https://github.com/Alexpux/MINGW-packages
   a) Clone the repository
   b) Change into mingw-w64-pygtksourceview2 directory of the repository
   c) Open a MSys64 or MSys32 bit console depending on the target you want to compile for
   d) Enter 
		
		MINGW_INSTALLS=mingw64 makepkg-mingw -sLf
	  
	  for 64-bit compilation in a 64 bit console or
		
		MINGW_INSTALLS=mingw32 makepkg-mingw -sLf
	 
	 for 32-bit compilation in a 32 bit console.

	 This will compile the package (you will need to download several developer tools in MSys
     via pacman, see what is requested during compilation)
	
 	 After compilation you find the stuff in the directory mingw-w64-i686-pygtksourceview2
	 of the pkg directory. Use its content as the content of the prebuilt packages mentioned above.
   
   Infos about installation of MinGW/MSYS: http://www.msys2.org/
   
   
4. Move the content of the bin directory of mingw32/mingw64 one level above and remove the empty 
   bin directory. The mingw32/ mingw64 directories should now contain the subdirs include, Lib, and 
   share and the content of the former bin directory.
   
5. Just for precaution:
   Compare the content of the mingw32 directory with the content of a fresh 32-bit Inkscape 
   installation (e.g. from a zip archive). Remove any duplicates from the mingw32 directory. 
   Repeat this with the mingw64 directory and a 64-bit installation of Inkscape. 
     
6. Build the file installation list using the Python script create_installer_file_lists.py
   In the script adapt the directory to use either files/mingw32 or files/mingw64 

7. Compile the installer script installer_pygtk_inkscape_0.9x using 
   nullsoft scriptable install system 3.03 (adapt the architecture flag in the script -> 32 or 64)

8. You will find the package in the build directory.