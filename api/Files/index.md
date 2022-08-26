# Files API

Welcome to the Files API!

This section is 100% related to Files, Console and System management across all available platforms that this engine supports. Its takes a big role in most parts of the entire engine API, and its a big part of the toolkit's overall functionality aswell.

This section is really long, and since its all functions, we're gonna split it into different categories based on different needs:

## Read and Write 101:

### std::string Read(const char* url)

**Requires**: A const array of characters.
**Returns**: A String.

This function is used to read overall files, it returns the content of the file that you set in the "url" parameter, in form of a string, containing everything, including end of files and tabs.

**Short Example**:

```cpp
... // Top code

// I want to load a .txt file that is located in the Game's folder.
// The name of it is "Hello.txt".

// Text Content:
// Hello from a .txt file! :D

std::string content = Files::Read("Game/HelloLetter.txt");

// Print the output.
std::cout << content << std::endl;

// Output:
// Hello from a .txt file! :D

... // Bottom code
```

### std::string Read(const char* url, bool isBinary)

**Requires**: A const array of characters.
**Returns**: A String.

The same thing as Read, but if the second parameter is set to true, it allows you to read binary files like executables, binary save files, etcetera.

**Short Example**:

```cpp
... // Top code

// For some odd reason, i have an executable called "SomeGame.exe"
// that is located in the same directory as my game, and i want 
// to print its content.

// If you set the 2nd boolean to false, it'll behave the same
// as the first Files::Read().
std::string content = Files::Read("SomeGame.exe", true);

// Print the output.
std::cout << content << std::endl;

// Output:
// (Bunch of glibberish)

... // Bottom code
```

### std::vector\<std::string\> ReadAndGetLines(const char* url)

**Requires**: One const array of characters.
**Returns**: One vector of strings.

This is like Files::Read(), with the difference that its going to split all of the lines of the file into a vector of strings.

**Short Example**:

```cpp
... // Top code

// I have an HTML file, and i want to separate the lines
// with a "======" for each line while printing the output.
// This file is going to be located in the "Game" folder.

// HTML Content:
// <html>
// 		<p>Hello!</p>
// </html>

std::vector\<std::string\> htmlLines = Files::ReadAndGetLines("Game/index.html");

// Now let's print the output, and add a "======" after
// printing a line.
for(auto i : htmlLines)
{
	std::cout << i << std::endl;
	std::cout << "======" << std::endl;
}

// Output:
// <html>
// ======
// 		<p>Hello!</p>
// ======
// </html>
// ======

... // Bottom code
```

### std::string Write(const char* url, std::string content)

**Requires**: A const array of characters and a String.
**Returns**: A String.

This is a function used to write files. You set the path of where the file is going to be written in the first parameter, and then set the contents of the file in form of a string in the second parameter.

**Short Example**:

```cpp
... // Top code

// I have this little string, that i want to save in a file
// as a .txt file.
std::string niceString = "I have a nice string here!"

// Now that we have the string, let's use the function
// to save it as a file.
Files::Write("NiceString.txt", niceString);

// Output of NiceString.txt:
// I have a nice string here!

... // Bottom code
```

### std::string Write(const char* url, std::string content, bool isBinary)

**Requires**: A const array of characters, a String and a boolean.
**Returns**: A String.

The same as above, but in binary mode. Can be used to modify executables or getting overall binary data into a file.

**Short Example**:

```cpp
... // Top code

// I have a function that is going to save some binary data
// that i have save in the RAM.
void SaveBinaryData(std::string& content)
{
	... // Do the thing.
}

... // More code


// Now we initialize an empty string, and put the contents
// inside of it.
std::string binaryData;
SaveBinaryData(binaryData);

// Once we have the binary content, we can save it as
// a file, in this case, we're going to save as "output.bin"
Files::Write("output.bin", binaryData, true);

... // Bottom code
```

### std::string Replace(const char* oldFile, const char* newFile)

**Requires**: Two const array of characters.
**Returns**: A String.

This is used to change the file's location. Basically "cut and paste" from one folder to another.

**Short Example**:

```cpp
... // Top code

// I have a .txt file that is currently located in my "Game"
// folder, but i want to move it to the executable's directory.
Files::Replace("Game/file.txt", "file.txt");

... // Bottom code
```

### std::string Replace(const char* oldFile, const char* newFile, bool isBinary)

**Requires**: Two const array of characters and a boolean.
**Returns**: A String.

The same as above, but in binary mode.

**Short Example**:

```cpp
... // Top code

// I have an .exe file that is currently located in my "Game"
// folder, but i want to move it to the executable's directory.
Files::Replace("Game/app.exe", "app.exe", true);

... // Bottom code
```

### bool Rename(const char* oldFile, const char* newFile)

**Requires**: Two const array of characters.
**Returns**: A String.

This function allows you to change the name of a file.

**Short Example**:

```cpp
... // Top code

// I have a .txt file that i want to change the name to
// something else.
Files::Rename("Game/file.txt", "Game/cookingRecipe.txt");

... // Bottom code
```
### std::string OpenImage(const char* url, int& width, int& height);

**Requires**: A const array of characters, and two integers.
**Returns**: A String, containing the image data.

This function allows you to read image data.

**Short Example**:

```cpp
... // Top code

//I have a .png file which i know the width and height 
//that I want to read the data from.
int width = 16;
int height = 16;
std::string billyData = Files::OpenImage("Game/billy.png", width, height);

... // Bottom code
```

### std::vector\<std::string\> OpenTexturePack(const char* gtxp);

> uhhhhhhhh what's this supposed to be?
> -#Guigui

### bool Remove(const char* url);

**Requires**: A const array of characters.
**Returns**: A boolean.

This function removes the file at desired file path.

```cpp
... // Top code

//I have a .txt file I want to remove.
Files::Remove("Game/meanwords.txt");

... // Bottom code
```

### std::vector\<unsigned char\> GetImageData(const char* url, int& width, int& height);

Same as `OpenImage()`, but instead of an `std::string`, it's an `std::vector` full of unsigned chars that gets returned.

### bool SaveImage(std::string output, std::vector<unsigned char> data, int width, int height);

**Requires**: A string, a vector of unsigned chars, and two integers.
**Returns**: A boolean.

This function saves image data to a file.

```cpp
... // Top code

// I have a vector of unsigned chars (called "data") containing modified image data of a 256*256 image, and want to save it to a file.
Files::SaveImage("newfile.png", data, 256, 256);

... // Bottom code
```

### std::vector\<float\> ReadOBJ(const char* url);

**Requires**: An array of chars.
**Returns**: A vector of floats.

Reads an .obj file and returns a vector of floats, containing vertex data

> TODO: what's it supposed to be help

## Directory & ZIP Management:

### void CreateDirectory(const char* url);

**Requires**: An array of chars.
**Returns**: Nothing.

This function creates a directory in the specified location.

```cpp
... // Top code

// I want to create a folder in the Game directory.
Files::CreateDirectory("Game/NewFolder_9999");

... // Bottom code
```

### void CopyDirectory(const char* url, const char* dest);

**Requires**: Two arrays of chars.
**Returns**: Nothing.

This function copies the specified directory into the specified destination.

```cpp
... // Top code

// I want to copy a folder to another place.
Files::CopyDirectory("Game/DO_NOT_LOSE_THIS_DATA", "Backup/ImportantData");

... // Bottom code
```

### void DeleteDirectory(const char* url);

**Requires**: An array of chars.
**Returns**: Nothing.

This function deletes the specified folder.

```cpp
... // Top code

// I want to delete a folder.
Files::DeleteDirectory("SomeUnneededFolder");

... // Bottom code
```

### bool DirectoryExists(const char* url);

**Requires**: An array of chars.
**Returns**: A boolean.

This function tells you whether a directory exists or no.

```cpp
... // Top code

// Let's say I want to check if a folder exists before checking the files inside:
if(Files::DirectoryExists("CoolFolder")){
	... //Code related to do stuff with the contents of the folder
}else{
	std::cout << "No folder named \"CoolFolder\" to be seen! :(" << std::endl;
}
... // Bottom code
```

### std::string GetDirectoryOf(const char* file);

**Requires**: An array of chars.
**Returns**: A string.

Removes the filename from the directory path. Could be useful to get a folder from a full path.

```cpp
... // Top code

//Let's say I need to get the directory of some file 
std::cout << Files::GetDirectoryOf("Path/To/SomeFile.txt") << std::endl;

//Output: Path/To/

... // Bottom code
```

### std::string GetFilenameFromDirectory(const char* dir);

**Requires**: An array of chars.
**Returns**: A string.

Retrieves the filename from a directoory path, and returns it. Basically the opposite of `GetDirectoryOf()`.

```cpp
... // Top code

//Let's say I need to get the directory of some file 
std::cout << Files::GetFilenameFromDirectory("Path/To/SomeFile.txt") << std::endl;

//Output: SomeFile.txt

... // Bottom code
```


### int UnZIP(const char* url, [OPTIONAL] std::string discardFolderEx);

**Requires**: An array of chars, and optionally a string.
**Returns**: An integer.

Unzips the specified ZIP file. [EXPERIMENTAL] You can provide a path to a folder to discard, like if for example everything in the zip is in a subfolder, you can put the path to that main folder from within the zip.

```cpp
... // Top code

//Unzip a zip file
Files::UnZIP("main.zip");

//Unzip a zip file, but the zip is constitued like this:
// /
// - /something/
//   - /something/everything.txt
//and we want to remove the /something/ folder so that everything in that folder is unzipped.
Files::UnZIP("main.zip", "/something");
```

### std::string GetGamePath();

**Requires**: Nothing!
**Returns**: A string.

Allows you to get the game's path.

```cpp
... // Top code

// I would like to print out the game path:
std::cout << Files::GetGamePath() << std::endl;

... // Bottom code
```

## Console functions:

### std::string WhereIs(std::string name);

**Requires**: A string.
**Returns**: Another string.

The equivalent of the "where" command on Windows, or "which" on Linux.

TODO: FINISH THIS WITH AN EXAMPLE IM LAZY OK

```cpp
... // Top code


... // Bottom code
```

### std::string RunCommand(std::string cmd);

**Requires**: A string.
**Returns**: Another string.

Runs the specified command, and returns its output.

```cpp
... // Top code

// This just runs an example command, and displays information from its output.
std::string output = Files::RunCommand("whoami");
std::cout << "Hello, " << output << "!" << std::endl;

... // Bottom code
```
### std::string GetValueFromCommand(std::string cmd);

**Requires**: A string.
**Returns**: Another string. (I'm starting to notice a pattern.)

Runs the specified command, and returns its output.
```cpp
... // Top code

// This will print the output of the "ls" command
std::cout << Files::GetPathFromCommand("ls") << std::endl;

... // Bottom code
```

### std::string GetPathFromCommand(std::string cmd);

**Requires**: A string.
**Returns**: Another string. (Again?!)

Same as `GetValueFromCommand`, but only returns it if the output is a valid path.

```cpp
... // Top code

//Get current active path through this method
std::cout << Files::GetPathFromCommand("cd") << std::endl;

... // Bottom code
```

## System & App Management:

### void ClearConsole();

**Requires**: Nothing.
**Returns**: And nothing!

This function clears the console.

```cpp
... // Top code

//Clear the console, now!
Files::ClearConsole();

... // Bottom code
```

### void HideConsole();

**Requires**: Nothing.
**Returns**: And nothing! (Another pattern, lmao)

Hides the console, if currently visible. **[CURRENTLY WINDOWS ONLY]**

```cpp
... // Top code

// The console is not needed anymore, hide it!
Files::HideConsole();

... // Bottom code
```

### void ShowConsole();

**Requires**: Nothing.
**Returns**: And nothing!

Shows the console, if hidden previously. **[CURRENTLY WINDOWS ONLY]**

```cpp
... // Top code

// Show the console, I just printed something useful!
Files::ShowConsole();

... // Bottom code
```

### void PauseConsole();

**Requires**: Nothing.
**Returns**: And nothing!

Pauses the console, and will resume process once enter has been pressed in the console.

```cpp
... // Top code

// I really have nothing to explain here.
Files::PauseConsole();


std::cout << "Unpaused!" << std::endl; // Won't be shown until Enter has been pressed.

... // Bottom code
```

### void ChangeCurrentDirectory(std::string path);

**Requires**: A string.
**Returns**: Nothing.

Goes to the desired directory. Apparently doesn't work on Linux yet. 

```cpp
... // Top code

// Switches to the Game directory
Files::ChangeCurrentDirectory("./Game");

... // Bottom code
```

### std::string GetExecutablePath();

**Requires**: Nothing.
**Returns**: A string.

Returns the current executable's path.

```cpp
... // Top code

// Prints executable path.
std::cout << Files::GetExecutablePath() << std::endl;

... // Bottom code
```
