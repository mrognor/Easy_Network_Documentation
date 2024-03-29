# Usefull library functions

[New page:](_e_n___functions_8h.html)

## GetIpByURL
`std::string GetIpByURL(std::string url)`
Function for getting an ip address from a url
* The first parameter is url

## Split  
`std::vector<std::string> Split(std::string StringToSplit, std::string SplitterString=" ")`  
The function is needed for convenient work with incoming messages. 
Designed to split a string into a vector of strings. 
Divides by spaces by default, but you can set your own line for separation. If there is a separator string at the end, then there will be an empty string at the end of the vector  

## SendFile  
`bool SendFile(EN_SOCKET FileSendSocket, std::string FilePath, bool& IsStop, void (*ProgressFunction)(uint64_t current, uint64_t all, uint64_t speed, uint64_t eta) = nullptr, uint64_t PreviouslySendedSize = 0, int ChunksNumberBetweenDelay = 0);`    
The function is needed to send files. The message receiving function should be called on the other side.  
* The first parameter is the socket for sending files  
* The second parameter is the full path to the file to be sent  
* The third parameter is a reference to a boolean variable to stop file transfer  
* The fourth parameter is a pointer to a function that is used to track the status of file transfer This function gets 4 parameters.  
	* The first is how many bytes were transmitted.  
	* The second is the total number of bytes.  
	* The third parameter shows the transfer rate in bytes.  
	* The fourth shows the remaining time in seconds  
* The fifth parameter is needed to continue downloading. Gets the size of the previously transmitted file in bytes. 0 means no previosly sending
* The sixth parameter is needed to regulate the file transfer rate. Gets amount of chunks between sending delay. 0 means no delay. The delay between sending the chunks is 20 millimeconds.

By default, the library function is used to output to the console  
Timeout between sending set to 20. You adjust the number of chunks that will be sent between the delay

## RecvFile  
`bool RecvFile(EN_SOCKET& FileSendSocket, bool& IsStop, void (*ProgressFunction)(uint64_t current, uint64_t all, uint64_t speed, uint64_t eta) = nullptr)`    
The function is needed to receiving files.  
* The first parameter is the socket for receiving files  
* The second parameter is a reference to a boolean variable to stop file transfer 
* The fourth parameter is a pointer to a function that is used to track the status of file transfer This function gets 4 parameters.  
	* The first is how many bytes were transmitted.  
	* The second is the total number of bytes.  
	* The third parameter shows the transfer rate in bytes.  
	* The fourth shows the remaining time in seconds  


By default, the library function is used to output to the console

## ContinueRecvFile  
`bool ContinueRecvFile(EN_SOCKET FileSendSocket, bool& IsStop, void (*ProgressFunction)(uint64_t current, uint64_t all, uint64_t speed, uint64_t eta) = nullptr)`  
Function to continue receiving the file
* The first parameter is the socket for receiving files  
* The second parameter is a reference to a boolean variable to stop file transfer 
* The fourth parameter is a pointer to a function that is used to track the status of file transfer This function gets 4 parameters.  
	* The first is how many bytes were transmitted.  
	* The second is the total number of bytes.  
	* The third parameter shows the transfer rate in bytes.  
	* The fourth shows the remaining time in seconds  

By default, the library function is used to output to the console  

## ForwardFile  
`bool ForwardFile(EN_SOCKET SourceFileSocket, EN_SOCKET DestinationFileSocket, bool& IsStop, void (*ProgressFunction)(uint64_t current, uint64_t all, uint64_t speed, uint64_t eta) = nullptr)`  
This function will forward file from one socket to another.  
* First parametr is source socket
* Second parametr is destination socket
* Third parametr its refernce to bool to stop transmission. 
* The fourth parameter is a pointer to a function that is used to track the status of file transfer This function gets 4 parameters.  
	* The first is how many bytes were transmitted.  
	* The second is the total number of bytes.  
	* The third parameter shows the transfer rate in bytes.  
	* The fourth shows the remaining time in seconds  

By default, the library function is used to output to the console  

## DownloadStatus  
`void DownloadStatus(uint64_t current, uint64_t all, uint64_t speed, uint64_t eta)`
The function displays the status of the file transfer to the console
* The first is how many bytes were transmitted.  
* The second is the total number of bytes.  
* The third parameter shows the transfer rate in bytes.  
* The fourth shows the remaining time in seconds  

## IsFileExist  
`bool IsFileExist(std::string FilePath)`  
Return true if file exists, otherwise rerurn false

## GetFileSize  
`uint64_t GetFileSize(std::string FileName)`
Return file size in bytes. If couldn't open the file return 0
	
## Delay
`void Delay(int milliseconds)`  
Crossplatform function for program suspension. Gets milliseconds. 

## IntToString
`std::string IntToString(int n)`
Function to convert int to string. 
* int number to convert  

One char takes 1 byte, and a int takes 4 bytes.
If you try to translate the number 120 into a string, then you will have 3 characters or 3 bytes. 
This function turns a number into a character, since a character occupies a byte, 
then you can transfer numbers up to 255 in one byte. 
This function can be considered as the translation of a number into a number system with a base of 256
This function does not work with negative numbers.

## StringToInt
`int StringToInt(std::string str)`
Function to convert string to int.
* string to convert to int  

Works with strings from function EN::IntToString.
Note that since the number is converted to a string, some digits may become spaces. 
This is important because problems may occur when using the Split function. 
For example, you divide a string by spaces and the function will divide your number into 2 lines  