Hello welcome to my worlde solver!!!


In this file



Describe your high level approach:
1. The Network Aspect:
I first read in the command line arguements and filter out intial commands, flags, northeastern username, and hostname. I then call my mega-main method which hosues the entire runtime operation. I initialize global variables (to avoid having methods constantly return new variable, and instead mutating objects which python does easily for global variables). Then send my inital message and enter a while loop which handles the 4 possible messages I can receive from the socket. Most of my helper methods like receiveMessage, sendMessage, connectToServer are basic or standard ways i found on the internet to do this. 
2. I have a list of words and take the first one (ranking will be discussed below), and sending it to the server, then running the loop again to see the servers response. Appropriate network methods are called in these parts.
3. Keep doing 2 and updating the possible words left until I get the answer or error. 

Describe any challenges you faced:
1. I didn't know any aspect of the networking code. I had to learn it conceptually first then find its implemenation online since we don't really cover this. Now though, it makes a lot of sense and seems reletivly straight forward after implementing it. 
2. Debugging. I'm somewhat comfortable with the debugger in Intelij from OOD, but I wanted to use python for this project (since I didn't want to code 1000 lines and 400 classes), which needed a different IDE/ text editior. I used pycharm eventually after trying VSCode since pycharm is made by the same people as intellij so the debugger was the exact same.
3. Getting the implementation of my guess approach to actually work. My idea made sense on paper but was very difficult to get working in code. Also, working around edge cases which was determined by the server was an issue here. Especially with words with two letters and one of them returned a 1 or 2. Like 'eeten', [0, 2, 0, 0, 1] which posed a lot of challenges and ended up breaking my approach for words with 5 unique letters.


Describe the guessing strategy your client implements:
1. Word Weight
I thought about having a weight associated to each word and sort the list based on most frequenctly used letters. So 'eeten' is going to have a higher value than 'quick' since e is the most common letter in the english language. What I thought about here was how words in scrabble have different points since your using common vs rare letters (inverse point score here) 

Therefore, to save compute time, I stored each word and its value in a hashmap, then sorted by the weight the word has. The words at the top have a higher weight. 

2. Heuristics
Starting off, each spot has 26 possible options. When I guess the highest value word (first in the list), I check each positon to see if that letter should or shouldn't be in it. Based on the response, I either keep it, remove it, or make it the only letter possible. This maps to getting a 1, 0, and 2 respectivley. So after running this, I now check every word to see if at each position, the letter in the word is within the list of possible letters for that spot. 

3. After applying Heuristics and get a guess
I now guessed based on the data from the last guess. Now, the remainning letters are then re-weighted but only on the spots not found. My reasoning behind this is that if I have 2/5 spots left, I want to guess a word which uses more common letters since that possibly eliminates more words if we find they aren't in the answer. 

4. Repeat 2 and 3 until you get the asnwer.

Describe an overview of how you tested your code:
1. Pycharm Debugger
I set break points inside of methods I was writting, then called the methods locally to step though them to ensure they did what I wanted them to do.

2. So many print statments.
As said above, I called the methods locally. I didn't have to worry about if the network/json parsing was wrong, just the core fuinctionality. So I added so many print statments inside the code at certian points to avoid using debuggers sometimes when I felt it wasn't needed. 

3. Call the sever and gradescope
The part that required a correct config for gradescope meant I had to keep tweaking end-line characters (windows vs linux), command line argument handlers, makefile etc. This had nothing to do with the code itself working and more to do with making it fit to the assignment specs. 


