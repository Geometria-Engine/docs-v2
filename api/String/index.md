# String API

Welcome to the String API!

This is mostly used to do string parsing, checking and overall manipulation of text.

## Functions:

### std::string ReplaceAll(std::string str, const std::string& from, const std::string& to)

**Requires**: Three Strings.
**Returns**: One String.

This function takes one string *(first parameter)*, and converts all of the parts of the string that match the *second parameter* to the *third parameter*.

**Short Example**:

```cpp
... // Top code

std::string sentence = "this is a big sentence and this is amazing!";

// Replace "this is" with "this is not".
sentence = StringAPI::ReplaceAll(sentence, "this is", "this is not");

// Output: "this is not a big sentence and this is not amazing!"

... // Bottom code
```

### std::string RemoveAll(std::string str, const std::string& del)

**Requires**: Two Strings.
**Returns**: One String.

Gets the *first parameter* and removes every substring that matches the *second parameter*.

**Short Example**:

```cpp
... // Top code

std::string sentence = "I don't have a dog, and i don't have a cat.";

// Remove all of the "don't"s in the sentence
sentence = StringAPI::RemoveAll(sentence, "don't ");

// Output: "I have a dog, and i have a cat."

... // Bottom code
```

### std::string GetSubstringBetween(std::string text, std::string first, std::string last)

**Requires**: Three Strings.
**Returns**: One String.

Grabs the *text* string, and tries to grab a portion of it between the *first* and *last* parameters.

This is useful to grab values inside a config file, for example.

**Short Example**:

```cpp
... // Top code

std::string sentence = "My name is Billy! Nice to meet you! :D";

// Get the name inside this sentence.
// We don't need to type the rest of it at the end, as long as it has a reference.
std::string getName = StringAPI::GetSubstringBetween(sentence, "My name is ", "! Nice");

// Output: Billy.

... // Bottom code
```

### std::vector\<std::string\> SplitIntoVector(const std::string& s, const char* c)

**Requires**: One String and one const array of characters.
**Returns**: One Vector of Strings.

Grabs the *first string parameter*, and splits it by using the *second parameter* as a reference, turning it into a vector/list.

**Short Example**:

```cpp
... // Top code

// We have this shopping list of things to buy, and we want to convert them into a list of strings.
std::string shoppingList = "Flowers|Watter Bottles|Eggs|Bananas|Lettuce";

// Since the list is divided by "|", we use it as a reference.
std::vector<std::string> finalList = StringAPI::SplitIntoVector(shoppingList, "|");

// Print the output.
for(auto i : finalList)
	std::cout << i << std::endl;

// Output:
// Flowers
// Watter Bottles
// Eggs
// Bananas
// Lettuce

... // Bottom code
```

### std::vector\<std::string\> GetLinesFromString(std::string s)

**Requires**: One String.
**Returns**: One Vector of Strings.

Gets the string input and divides it by using the end lines (or "\n") as a reference.

This can be useful to parse code or configuration files.

**Short Example**:

```cpp
... // Top code

// Let's suppose that i have a letter, and i need to take out mean things.
std::string letter = Files::Read("NiceLetter.txt");

// Input:
// I love dogs!
// I hate cats!
// I love popcorn!
// I hate Billy!

// First, let's split the lines into a vector.
std::vector<std::string> letterLines = StringAPI::GetLinesFromString(letter);

// And then run a for loop, printing out only the lines that contain "love".

for(auto i : letterLines)
{
	// Check if the item contains the word "love".
	if(i.find("love") != std::string::npos)
		std::cout << i << std::endl;
}

// Output:
// I love dogs!
// I love popcorn!

... // Bottom code
```

### bool StartsWith(std::string string, std::string starts)

**Requires**: Two Strings.
**Returns**: One boolean.

This function checks if the *first parameter* "string", starts like the *second parameter* "starts".

**Short Example**:

```cpp
... // Top code

// Let's suppose that you don't agree with this sentence
// and you don't want to print it.
std::string sentence = "I think its a good idea to go for a walk at 2AM.";

// If you do this check, its not going to print anything.
if(StringAPI::StartsWith(sentence, "I don't think"))
	std::cout << sentence << std::endl;

// Now let's change the sentence.
sentence = "I don't think its a good idea to go for a walk at 2AM.";

// If you do the check again, the sentence is going to be printed to the console.
if(StringAPI::StartsWith(sentence, "I don't think"))
	std::cout << sentence << std::endl;

// Output: I don't think its a good idea to go for a walk at 2AM.

... // Bottom code
```

### bool EndsWith(std::string string, std::string ends)

**Requires**: Two Strings.
**Returns**: One boolean.

This function checks if the *first parameter* "string", ends like the *second parameter* "ends".

**Short Example**:

```cpp
... // Top code

// I want to say that i have four bananas.
std::string sentence = "I have four bananas.";

// But there's a problem, i need six bananas.
// So i can't print it, since this check is going to be false.
if(StringAPI::EndsWith(sentence, "six bananas."))
	std::cout << sentence << std::endl;

// Now let's change the sentence.
sentence = "I have six bananas.";

// If you do the check again, the sentence is going to be printed to the console.
if(StringAPI::EndsWith(sentence, "six bananas."))
	std::cout << sentence << std::endl;

// Output: I have six bananas.

... // Bottom code
```

### bool IsOnlyDigits(const std::string &str)

**Requires**: One String.
**Returns**: One boolean.

Checks if the parameter only has digits.
If it has atleast one letter or ASCII character, it'll return false.

```cpp
... // Top code


// I have two codes, but i want to print 
// the simple one and keep the complex for
// later.
std::string simpleCode = "29384352";
std::string complexCode = "s8nr29fskd*";

// Since "complexCode" has letters and other
// characters, its not going to print.
if(StringAPI::IsOnlyDigits(complexCode))
	std::cout << complexCode << std::endl;

// But if we run this check in the "simpleCode",
// since its only made out of numbers, it'll print it.
if(StringAPI::IsOnlyDigits(simpleCode))
	std::cout << simpleCode << std::endl;

// Output: 29384352

... // Bottom code
```