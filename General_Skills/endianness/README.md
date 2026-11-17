# Endianness

The problem tells us to find the big-endian and little-endian format of a given word.

Process:
1. Find the ascii value of each character in the word.
2. Convert the ascii values to hexadecimal.
3. Determine the byte order for big-endian and little-endian formats.
E.g If word is "ABCD", the ascii values are:
- A: 65 (0x41)  
- B: 66 (0x42)
- C: 67 (0x43)  
- D: 68 (0x44)
- Big-endian format: 0x41 0x42 0x43 0x44
- Little-endian format: 0x44 0x43 0x42 0x41

The final output for the word "ABCD" would be:
- Big-endian: 41424344    
- Little-endian: 44434241
  
Lessons Learned: Understanding endianness is crucial in computer architecture and data representation. It affects how data is stored and interpreted in memory, which can lead to issues in cross-platform data exchange if not handled correctly.