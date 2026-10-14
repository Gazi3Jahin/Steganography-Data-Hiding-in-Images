Image Steganography — Visualizing Hidden Data in Images

A lightweight Python project that hides text messages inside digital images using Least Significant Bit (LSB) steganography. The project implements three message-encoding methods and provides visualizations that reveal where data is stored, which pixel channels are modified, and how the encoded image differs from the original.

Built entirely in Google Colab, this project requires no backend, frontend, model training, or complex setup.

Project Overview

Image steganography conceals information within digital media. Rather than visibly displaying a secret message, this project embeds its binary representation into the least significant bits of an image's RGB pixel channels.

The notebook supports raw UTF-8, Base64, and XOR-transformed messages, alongside decoding, verification, and detailed visual analysis.

Key Features

1. Multiple Encoding and Decoding Methods

Raw UTF-8 + LSB: Embeds the original message as UTF-8 bytes.

Base64 + LSB: Encodes the message into Base64 before embedding it.

XOR + LSB: Applies a reversible XOR transformation before hiding the message.

Each method uses the same LSB embedding and extraction mechanism, allowing their payload sizes and behavior to be compared.

2. Hidden-Data Location Visualization

Visualize where the message is stored within the image.

Generate a spatial map of pixels used for data embedding.

Display the number of RGB channels used per pixel.

Distinguish the 32-bit message-length header from the message payload.

Identify the actual pixel coordinates associated with embedded bits.

3. Pixel-Level Change Analysis

Compare the original and encoded images to understand the visual impact of embedding.

Display original and encoded images side by side.

Amplify pixel differences to reveal subtle modifications.

Compare original and modified pixel-channel values.

Inspect individual embedded bits and their corresponding RGB channels.

4. Binary and Bit-Plane Visualization

Explore the binary structure of digital images.

Visualize individual bit planes of the red channel.

Compare pixel values before and after encoding.

Understand how least significant bits represent hidden information.

5. Message Extraction and Verification

Extract the stored payload from an encoded image.

Decode the payload using the corresponding method.

Verify whether the recovered message matches the original input.

Download the encoded image as a PNG file.

How It Works

The project follows this pipeline:

Upload: Load a PNG or JPG image into Google Colab.

Enter message: Provide the text to hide.

Transform: Select raw UTF-8, Base64, or XOR processing.

Embed: Store the message length and payload bits in RGB pixel channels.

Visualize: Inspect the embedding locations, header, payload, and pixel differences.

Extract: Recover the hidden bytes from the encoded image.

Decode: Reverse the selected message transformation.

Verify: Compare the recovered text with the original message.

Export: Download the encoded image in PNG format.

Understanding LSB Steganography

An RGB image stores each color channel as an 8-bit value between 0 and 255.

For example:

Original pixel-channel value:  11001010  (202)
Hidden bit:                    1
Modified pixel-channel value:  11001011  (203)

Only the least significant bit changes. The numerical difference is at most one per modified channel, making the change generally difficult to notice visually.

Message Storage Layout

The implementation uses sequential embedding:

Component

Description

Header

First 32 bits encode the payload length in bytes.

Payload

Following bits contain the encoded message.

Storage order

RGB channels, traversed sequentially from the top-left pixel.

The location visualization marks pixels used by the header and payload. A pixel can contain data in one, two, or all three RGB channels.

The map indicates where the algorithm writes data, even if a particular channel's least significant bit already matches the intended message bit.

Visualizations

The notebook includes the following visual outputs:

Visualization

Purpose

Original vs. encoded image

Compare the visual appearance before and after embedding.

Hidden-data location map

Identify pixels whose channels store embedded bits.

Header and payload map

Distinguish message-length metadata from message content.

Pixel-difference map

Amplify changes introduced during encoding.

Pixel-channel comparison

Inspect original and modified values.

Bit-plane analysis

Explore the binary representation of image channels.

Embedded-bit table

Show bit positions, pixel coordinates, channel names, and before/after values.

Together, these visualizations connect the hidden binary data to its physical storage locations within the image.

Technologies Used

Python — Core implementation.

NumPy — Pixel-array manipulation and binary operations.

Pillow (PIL) — Image loading, conversion, and PNG export.

Matplotlib — Image comparison, heatmaps, and bit-plane visualization.

Google Colab — Notebook execution and file uploads.

Base64 — Message encoding.

XOR operations — Reversible byte transformation.

Getting Started

Requirements

A Google account and a web browser are sufficient. All processing can be performed in Google Colab without local installation.

Running the Project

Open Google Colab.

Create a new Python notebook.

Copy the project code cells into the notebook in order.

Upload an image using the first cell.

Enter a secret message and an XOR key when prompted.

Run the encoding and decoding cells.

Explore the image comparison and hidden-data visualizations.

Select an encoded image and download the resulting PNG.

Input and Output

Input: A digital image and a text message.

Supported image input: Common formats supported by Pillow, including JPG and PNG.

Encoded output: PNG.

Decoding output: The recovered text message.

PNG is recommended for encoded images because lossless storage preserves the pixel values required for successful extraction. Saving an encoded image as JPEG may destroy hidden data.

Limitations and Security Considerations

Capacity: The maximum payload depends on the number of image channels available. The 32-bit header also consumes embedding capacity.

Image transformations: Resizing, lossy compression, or other pixel-changing operations may corrupt the embedded message.

Base64: Base64 is an encoding format, not encryption.

XOR: The repeating-key XOR method is a demonstration of reversible transformation, not secure encryption.

Detectability: Basic LSB embedding does not guarantee that hidden data cannot be detected.

Authentication: The implementation does not provide cryptographic authentication or tamper protection.

This project is intended for educational and experimental purposes. It demonstrates data hiding and image analysis rather than providing a secure communication system.

Future Improvements

Potential extensions include:

Measuring image quality using Mean Squared Error (MSE) and Peak Signal-to-Noise Ratio (PSNR).

Comparing embedding capacity across image sizes and color channels.

Supporting text-file embedding and extraction.

Exploring alternative embedding strategies and randomized storage positions.

Adding authenticated encryption before embedding.

Evaluating robustness against image processing and compression.

Learning Outcomes

This project demonstrates practical applications of:

Image processing and RGB pixel manipulation.

Binary data representation and bitwise operations.

Information hiding and message recovery.

Reversible encoding transformations.

Visual analysis of pixel-level modifications.

Capacity, image quality, and steganographic limitations.


##Author##
G.T.S. Jahin
