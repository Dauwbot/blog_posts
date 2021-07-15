---
layout: ../../layouts/thoughtPost.astro
title: Developing a password generator
abstract: I've been generating password with brain.exe for too long! Let's automate it!
categories: 
- C#
published: true
date: 20210715
---
## TLDR: I want the repo!

The code explained in this article is available at [https://github.com/Dauwbot/passwordCreator](https://github.com/Dauwbot/passwordCreator). Have fun.

## Introduction
Passwords are everywhere, we're encouraged to create a different one for each website, they've to have a certain level of complexity. I got fed up and decided to follow the [xkcd method](https://xkcd.com/936/) for quite some times, it works more often than not, damn website wanting special characters and numbers are sometimes a pain to deal with: tell us before we enter the password what you want! And I'm sick of [recommended passwords policies](https://its.lafayette.edu/policies/strongpasswords/).

Even if I've to create a password like that it'll either way be stocked in my Keepass dictionnay which use a *kind off* secure password. My whole life is there, if I came to pass my girlfriend knows the password, otherwise my Facebook wall would be full of RIP from person I've not talked with in years...

So, the process is not hard on my side but I sometime bug when trying to think of words on the spot and I wanted to automate it.

# Password generation using .TXT files
I decided to take the matter in my own hands. I had a clear idea of what I wanted to do. Generate a password with 3 words out of the French and English vocabulary and copy it to my clipboard without me having to do anything else than launch the program.
I settled on C# for this. I could've done it in any language but I feel like C# is the best candidate with my expertise and the fact that I want it to run on Windows & Unix based OS (Linux/MacOS).

So let's get to work (when I'm writing this the program is nearly done, *story-telling they call that!*)

## Acquiring datasets
First I had to get my *datasets* (new word entered in my dictionnary). I wanted both English and French words mixing so I used the following Google searches `words dataset` -> Which gave me access to this [bag of Words Data Set from UCI](https://archive.ics.uci.edu/ml/datasets/Bag+of+Words) & then searched for `liste mots français txt` and [grabbed a .txt file from freelang.com](https://www.freelang.com/dictionnaire/dic-francais.php).

## Cleaning data
After a quick inspection it appeared that my French words datasets where using accentuation (or as I've since learned to know them as *diacritics*, man lots of new words today!) and since I'm using a QWERTY layout that would be a pain to deal with, having to ALT + SPACE to switch to French layout & getting my **é** & **è** is too much work.

So let's clean those out. It appears that people **ABSOLUTELY LOVES** to just **REMOVE** the diacritics and keep the word, which is an heresy.

![Scene from Kaamelot where a monk scream "At the stake"](https://nsa39.casimages.com/img/2018/02/14/180214102154578617.gif)

I wanted to remove them, there was a lot of topics about that on StackOverflow, none where what I wanted.
I settled to read each line of the file, `Normalize()` it, you [can check the Microsoft documentation](https://docs.microsoft.com/en-us/dotnet/api/system.string.normalize?view=net-5.0) but to make it clearer: it separates the character from it's accent.

What use in that? Because then you can switch over each character and use `CharUnicodeInfo.GetUnicodeCategory(char)` and if it is of the type `UnicodeCategory.NonSpacingMark` you then can ignore that line and go to the next.

![A man doing the magic sign with it's hand](https://thumbs.gfycat.com/SpicyHighlevelCavy-max-1mb.gif)

I also removed lines starting with `UnicodeCategory.UppercaseLetter` since I don't want People, countries or brands names in my passwords and finally removed `UnicodeCategory.DashPunctuation` to remove composed words which are somewhat frequent in French.

I then had to write the word if it didn't present any problem, I did that by checking if the current character position was the same length as our word. If yes & it's not a *diacritic* then I can add the word back using a `StreamWriter`. If you want more infos about that just check the repo.

## Add uppercase to each word
In an effort to already bullet proof myself for password requirements I re-added an UpperCase letter to each word in the file. It's easier to read also when you don't copy paste your password.
Lots of boiler plate code but the function doing it is a one liner, thanks Linq, `sw.WriteLine(line.First().ToString().ToUpper() + line.Substring(1));`

"Urgh what's this monstruosity?!" One it's my code, my child, you don't tell somebody it's toddler is hard to look at, do you? Two it read the line, select the `First()` element in it, makes sure it's a String and convert it `ToUpper()` before adding back the rest of the string to it. 

## Remove shorts and long words
If you check the code you will see that I've removed words from a certain length. In my case they're between 4 and 6 letters. Which leaves us with around 12k English words & 5k in French. I'm not that good in stats but that makes a lot of possibility when choosing 3 words each time, damn I spoiled the fact that I only made 3 words length passwords...

## Create our password
So now I'm left with 2 files to chose from, let's go with 3 words length for the password.

```
static List<string> ReadAllLinesFromFiles (string directoryPath) {
    int fCount = Directory.GetFiles(directoryPath, "*.txt", SearchOption.TopDirectoryOnly).Length;
    var random = new Random();
    int fileIndex = random.Next(fCount);
    string[] files = Directory.GetFiles(directoryPath, "*.txt", SearchOption.TopDirectoryOnly);
    string filePath = files[fileIndex];
    return File.ReadAllLines(filePath).ToList();
}
```

This *method* (we're doing OOP, our function is part of a class so it's a method), index our files in a directory and choose a random one. It's name is not that good then, I'll rename it right now (2.42PM on the 15th July 2021) to `ReadAllLinesFromRandomFileInDirectory`, so I don't need any kind of doc to explain what it does. It returns a List\<String> for easier randomization in the main loop.

### The main loop

```
static void Main(string[] args)
{
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < 3; i++ ){
        var list = ReadAllLinesFromRandomFileInDirectory("./sourceFiles/");
        var random = new Random();
        int index = random.Next(list.Count);
        sb.Append(list[index]);
    }
    Console.WriteLine(sb.ToString());
    TextCopy.ClipboardService.SetText(sb.ToString());
}
```

Too finish here's my main function. It select a random word from our random List and append it to a stringbuilder.
The interesting part is `TextCopy.ClipboardService.SetText(sb.ToString());`. It uses the `TextCopy` nuget package to copy our newly created password to our clipboard. And that in a system agnostic way. A big thank you to [Simon Cropp](https://stackoverflow.com/a/51912933/5449540) for the work done on this [open source project](https://github.com/SimonCropp/TextCopy) that allowed me to copy to the clipboard from my WSL2 installation without having to limit myself to Windows and the `Clipboard` class.

So that's it for now, there's still some work to do. Package the app, create a CLI to pass options to it like the number of words to use. I could add even more complexity by cutting files in multiple smaller ones so that the random is even more random! Oh well, *later*...