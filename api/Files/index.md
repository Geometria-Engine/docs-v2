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

std::vector<std::string> htmlLines = Files::ReadAndGetLines("Game/index.html");

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

This function llows you to change the name of a file.

**Short Example**:

```cpp
... // Top code

// I have a .txt file that i want to change the name to
// something else.
Files::Rename("Game/file.txt", "Game/cookingRecipe.txt");

... // Bottom code
```
