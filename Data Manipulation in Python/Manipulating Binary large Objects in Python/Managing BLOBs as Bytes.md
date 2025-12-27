# Managing BLOBs as Bytes

The term **BLOB** (Binary Large Object) refers to large binary data such as images, audio files, PDFs, or executables. In Python, we can read a BLOB exactly as we would read any binary file using the `"rb"` mode.

Python also supports several external libraries to help manipulate BLOBs, such as **Pillow (PIL)** and **wand**. In this topic, we will use **wand**, which provides powerful image-processing capabilities.

## Reading an Image File as a BLOB

Let us create a script called `blob1.py` that reads an image file into memory as raw bytes and then prints information about it.

### Corrected `blob1.py`

```
from wand.image import Image

fin = input("Enter image file: ")

with open(fin, "rb") as f:
    image_blob = f.read()

print("BLOB stored as:", type(image_blob))
print("Length of BLOB:", len(image_blob))

with Image(blob=image_blob) as img:
    print("Image size:", img.width, "x", img.height)
```

### Explanation

1. **Import** the `Image` class from the `wand.image` module.
2. **Prompt** the user for a filename.
3. Open the file in **binary mode** (`rb`).
4. Read the entire content into the variable `image_blob`.
5. Display its type (`bytes`) and size in bytes.
6. Use `Image(blob=image_blob)` to extract metadata such as dimensions.

### Example Output

```
~ % python3 blob1.py
Enter image file: random.jpg
BLOB stored as: <class 'bytes'>
Length of BLOB: 197011
Image size: 1920 x 1080
```

## Converting a JPG to PNG Using Wand

Next, we will use the wand library to convert an image from **.jpg** to **.png** format and save the result.

Let us create a second script, `blob2.py`.

### Corrected `blob2.py`

```
from wand.image import Image

fin = input("Enter image file: ")

# Generate output filename by replacing .jpg with .png
fout = fin.replace(".jpg", ".png")

# Read original file as raw bytes
with open(fin, "rb") as f:
    image_blob = f.read()

# Use wand to load, convert, and save the image
with Image(blob=image_blob) as img:
    img.format = "png"
    img.save(filename=fout)

print("Conversion complete:", fout)
```

### Explanation

- Line 3: The output filename is created by replacing the .jpg`` extension.
- Lines 6–7: The original file is read into `image_blob`.
- Lines 10–12: Wand loads the raw bytes and converts the internal format to PNG.
- Line 12: The image is saved with the new extension.

### Running the Conversion

```
~ % python3 blob2.py
Enter image file: random.jpg
Conversion complete: random.png
```

Now we check the PNG file using our earlier script:

```
~ % python3 blob1.py
Enter image file: random.png
BLOB stored as: <class 'bytes'>
Length of BLOB: 1052066
Image size: 1920 x 1080
```

Notice that the PNG version is significantly larger than the JPEG. This is normal because JPEG is a compressed (lossy) format, while PNG is lossless and usually larger.
