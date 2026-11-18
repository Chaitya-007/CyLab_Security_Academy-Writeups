RED

1] Get the file
```bash
wget <url_to_red_image> 
```

2] check the file type using `file` command to confirm it's a disk image.

```bash
file red.png
``` 
Output

```bash
red.png: PNG image data, 128 x 128, 8-bit/color RGBA, non-interlaced
```
This confirms that the file is a PNG image, which is not a disk image.

3] The meta-data contained a POEM. Upon checking the poem, it was found that the poem contained a hidden message. The message was encoded in the first letter of each line of the poem.

4] **CHECK LSB**

5] Use steganography tools to extract hidden data from the image. `zsteg` to analyze the PNG file for any hidden information.

```bash
zsteg red.png
```

6] The output of `zsteg` revealed encoded base64 string. Decode it using `base64` command to retrieve the hidden message.


zsteg is a command-line tool used to detect and extract hidden data (steganography) inside **PNG** and **BMP** image files. It is widely used in Capture the Flag (CTF) competitions, digital forensics, and cybersecurity investigations.

What It Checks For

• **Least Significant Bit (LSB) steganography**: Scans color channels (R, G, B, A) and bit combinations for hidden text, files, or flags.
• **Compressed and embedded payloads**: Detects zlib-compressed data, file signatures, and metadata.
• **Format-specific hidden data**: Checks PNG palettes/chunks and BMP headers or padding, as well as data hidden by tools like OpenStego or Camouflage


Key Limitations & Usage

• **Supported formats**: Works specifically on lossless **PNG** and **BMP** files. It is not meant for **JPEG images** because lossy compression alters pixel data and breaks LSB payloads.
• **Basic usage**: Run zsteg image.png in the terminal (or use **zsteg --all image.bmp** for a broader scan). You can also try a browser-based scanner like zsteg Online if you do not have Ruby installed locally.

