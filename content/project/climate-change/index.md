---
title: 'Climate change'
date: 2025-01-26
author: "Armstrong Foundjem"
tags:
  - Climate change 
  - Sustanability
  - Green code
---


```cpp
#include <iostream>
#include <vector>
#include <png.h>

void convertToGrayscale(const std::string& inputFileName, const std::string& outputFileName) {
    FILE* inputFile = fopen(inputFileName.c_str(), "rb");
    if (!inputFile) {
        std::cerr << "Error opening input image file." << std::endl;
        return;
    }

    png_structp pngPtr = png_create_read_struct(PNG_LIBPNG_VER_STRING, nullptr, nullptr, nullptr);
    if (!pngPtr) {
        std::cerr << "Error creating PNG read structure." << std::endl;
        fclose(inputFile);
        return;
    }

    png_infop infoPtr = png_create_info_struct(pngPtr);
    if (!infoPtr) {
        std::cerr << "Error creating PNG info structure." << std::endl;
        png_destroy_read_struct(&pngPtr, nullptr, nullptr);
        fclose(inputFile);
        return;
    }

    png_init_io(pngPtr, inputFile);
    png_read_info(pngPtr, infoPtr);

    int width = png_get_image_width(pngPtr, infoPtr);
    int height = png_get_image_height(pngPtr, infoPtr);
    int bitDepth = png_get_bit_depth(pngPtr, infoPtr);
    int colorType = png_get_color_type(pngPtr, infoPtr);

    if (bitDepth != 8 || colorType != PNG_COLOR_TYPE_RGB) {
        std::cerr << "Unsupported image format. Only 8-bit RGB images are supported." << std::endl;
        png_destroy_read_struct(&pngPtr, &infoPtr, nullptr);
        fclose(inputFile);
        return;
    }

    std::vector<unsigned char> imageData(width * height * 3);
    std::vector<std::vector<unsigned char> > inputImage(height, std::vector<unsigned char>(width * 3));

    for (int i = 0; i < height; ++i) {
        png_read_row(pngPtr, reinterpret_cast<png_bytep>(inputImage[i].data()), nullptr);
    }

    fclose(inputFile);
    png_destroy_read_struct(&pngPtr, &infoPtr, nullptr);

    // Convert to grayscale
    std::vector<std::vector<unsigned char> > outputImage(height, std::vector<unsigned char>(width));
    for (int i = 0; i < height; ++i) {
        for (int j = 0; j < width; ++j) {
            // Simple grayscale conversion formula: (R + G + B) / 3
            outputImage[i][j] = (inputImage[i][j * 3] + inputImage[i][j * 3 + 1] + inputImage[i][j * 3 + 2]) / 3;
        }
    }

    // Write output image
    FILE* outputFile = fopen(outputFileName.c_str(), "wb");
    if (!outputFile) {
        std::cerr << "Error opening output image file." << std::endl;
        return;
    }

    pngPtr = png_create_write_struct(PNG_LIBPNG_VER_STRING, nullptr, nullptr, nullptr);
    if (!pngPtr) {
        std::cerr << "Error creating PNG write structure." << std::endl;
        fclose(outputFile);
        return;
    }

    infoPtr = png_create_info_struct(pngPtr);
    if (!infoPtr) {
        std::cerr << "Error creating PNG info structure." << std::endl;
        png_destroy_write_struct(&pngPtr, nullptr);
        fclose(outputFile);
        return;
    }

    png_init_io(pngPtr, outputFile);
    png_set_IHDR(pngPtr, infoPtr, width, height, 8, PNG_COLOR_TYPE_GRAY, PNG_INTERLACE_NONE, PNG_COMPRESSION_TYPE_DEFAULT, PNG_FILTER_TYPE_DEFAULT);
    png_write_info(pngPtr, infoPtr);

    for (int i = 0; i < height; ++i) {
        png_write_row(pngPtr, reinterpret_cast<png_bytep>(outputImage[i].data()));
    }

    png_write_end(pngPtr, nullptr);
    png_destroy_write_struct(&pngPtr, &infoPtr);
    fclose(outputFile);

    std::cout << "Image processing complete. Grayscale image saved to " << outputFileName << std::endl;
}

int main() {
    std::string inputFileName = "input.png";
    std::string outputFileName = "output_grayscale.png";
    
    convertToGrayscale(inputFileName, outputFileName);

    return 0;
}
```



<!--more external_link: https://github.com/scikit-learn/scikit-learn-->
