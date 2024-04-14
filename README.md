# first-project
task 1
//Names and IDs: Ziyad Ayman Ahmed (20230574) / Shahed Azouz Ali (20230193) / Ahmed Ashraf Mohamed (20230006)
//section: sp 5,6
/*  Main filter parts
 Ziyad Ayman Ahmed:
Invert Image
Rotate Image
Frame Image
Blur image
 Shahed Azouz Ali:
Resize image
Crop image
Black and white image
Flip Image
 Ahmed Ashraf Mohamed:
Dark and bright image
Merge image
Greyscale image
Edge detect image
    Bonus filter parts
 Ziyad Ayman Ahmed: Infrared Filter
 Shahed Azouz Ali: Natural Sunlight Filter
 Ahmed Ashraf Mohamed: Purple Filter
 **********************************************
 SYSTEM DIAGRAM :https://drive.google.com/file/d/1RnAE3NCt13TNOCeOFmAHd_9FTgHnKRyd/view?usp=sharing
 */
//section: sp 5,6
#include <iostream>
#include <vector>
#include "Image_Class.h"
using namespace std;
void EdgeDetection(Image &gray, Image &edgeImage) {
    for (int i = 1; i < gray.width - 1; ++i) {
        for (int j = 1; j < gray.height - 1; ++j) {
            for (int k = 0; k < 3; ++k) {

                int gx = (gray(i+1, j-1, k) + gray(i+1, j+1, k) + 2*gray(i+1, j, k)) - (gray(i-1, j-1, k) + gray(i-1, j+1, k) + 2*gray(i-1, j, k));
                int gy = (gray(i-1, j+1, k) + gray(i+1, j+1, k) + 2*gray(i, j+1, k)) - (gray(i-1, j-1, k) + gray(i+1, j-1, k) + 2*gray(i, j-1, k));
                int mag = sqrt(gx*gx + gy*gy);


                if (mag > 128)
                    edgeImage(i, j, k) = 255; // White
                else
                    edgeImage(i, j, k) = 0; // Black
            }
        }
    }
}

void Invert(string & filename){
    Image image1(filename);
//        image1.loadNewImage("hello.jpg");
    for (int i = 0; i < image1.width; ++i) {
        for (int j = 0; j < image1.height; ++j) {
            for (int k = 0; k < image1.channels; ++k) {
                int px = image1(i, j, k);
                int rev = 255 - px;
                image1(i, j, k) = rev;
            }
        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    int choose;
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    if (1 == choose) {
        image1.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> filename;
        image1.saveImage(filename);
        system(filename.c_str());
    }
}
void Rotate(string & filename){
    Image image2(filename);
    int choice2;
    cout << "How do you want to rotate the image?" << endl;
    cout << "1 - 90 clockwise" << endl;
    cout << "2 - 180 clockwise" << endl;
    cout << "3 - 270 clockwise" << endl;
    int choice;
    while (true) {
        cin >> choice2;
        if (  choice2 == 1 || choice == 2 || choice == 3) {
            break;
        } else {
            cout << "Invalid input. Please enter a number from 1 to 3 " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    //90 degree
    if (choice2 == 1) {
        Image image90(image2.height, image2.width);
        for (int i = 0; i < image2.width; ++i) {
            for (int j = 0; j < image2.height; ++j) {
                for (int k = 0; k < image2.channels; ++k) {
                    image90(j, image2.width - 1 - i, k) = image2(i, j, k);
                }
            }
        }
        cout << "do you want save image with the same name(1)\n";
        cout << "want save image with new name(2)\n";
        int choose;
        while (true) {
            cin >> choose;
            if (choose == 1 || choose == 2) {
                break;
            } else {
                cout << "Invalid input. Please enter 1 or 2 : " << endl;
                cin.clear();
                cin.ignore();
            }

        }
        if (1 == choose) {
            image90.saveImage(filename);
            system(filename.c_str());
        } else if (2 == choose) {
            cout << "enter the new filename:\n";
            cin >> filename;
            image90.saveImage(filename);
            system(filename.c_str());
        }



    }
        //180 degree
    else if (choice2 == 2) {
        Image image180(image2.width, image2.height);
        for (int i = 0; i < image2.width; ++i) {
            for (int j = 0; j < image2.height; ++j) {
                for (int k = 0; k < image2.channels; ++k) {
                    image180(image2.width - 1 - i, image2.height - 1 - j, k) = image2(i, j, k);
                }
            }
        }
        cout << "do you want save image with the same name(1)\n";
        cout << "want save image with new name(2)\n";
        int choose;
        while (true) {
            cin >> choose;
            if (choose == 1 || choose == 2) {
                break;
            } else {
                cout << "Invalid input. Please enter 1 or 2 : " << endl;
                cin.clear();
                cin.ignore();
            }

        }
        if (1 == choose) {
            image180.saveImage(filename);
            system(filename.c_str());
        } else if (2 == choose) {
            cout << "enter the new filename:\n";
            cin >> filename;
            image180.saveImage(filename);
            system(filename.c_str());
        }

    }
        //270 degree
    else if (choice2 == 3) {
        Image image270(image2.height, image2.width);
        for (int i = 0; i < image2.width; ++i) {
            for (int j = 0; j < image2.height; ++j) {
                for (int k = 0; k < image2.channels; ++k) {
                    image270(image2.height - 1 - j, i, k) = image2(i, j, k);
                }
            }
        }
        cout << "do you want save image with the same name(1)\n";
        cout << "want save image with new name(2)\n";
        int choose;
        while (true) {
            cin >> choose;
            if (choose == 1 || choose == 2) {
                break;
            } else {
                cout << "Invalid input. Please enter 1 or 2 : " << endl;
                cin.clear();
                cin.ignore();
            }

        }
        if (1 == choose) {
            image270.saveImage(filename);
            system(filename.c_str());
        } else if (2 == choose) {
            cout << "enter the new filename:\n";
            cin >> filename;
            image270.saveImage(filename);
            system(filename.c_str());
        }

    }
}
void framed(string & filename) {
    Image image3(filename);

    int thickness;
    int red, green, blue;
    cout << "Enter frame thickness: ";
    while (true) {
        cin >> thickness;
        if (thickness > 0) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    cout << "Enter frame color (RGB values separated by spaces): ";
    while (true) {
        cin >> red >> green >> blue;
        if (red > 0 && green > 0 &&  blue >0 ) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    //left side
    for (int i = 0; i < thickness; ++i) {
        for (int j = 0; j < image3.height; ++j) {
            image3(i, j, 0) = red;
            image3(i, j, 1) = green;
            image3(i, j, 2) = blue;
        }
    }
    //top side
    for (int j = 0; j < thickness; ++j) {
        for (int i = 0; i < image3.width; ++i) {
            image3(i, j, 0) = red;
            image3(i, j, 1) = green;
            image3(i, j, 2) = blue;
        }
    }
    // Add frame to the right side
    for (int i = image3.width - thickness; i < image3.width; ++i) {
        for (int j = 0; j < image3.height; ++j) {
            image3(i, j, 0) = red;
            image3(i, j, 1) = green;
            image3(i, j, 2) = blue;
        }
    }

    // Add frame to the bottom side
    for (int j = image3.height - thickness; j < image3.height; ++j) {
        for (int i = 0; i < image3.width; ++i) {
            image3(i, j, 0) = red;
            image3(i, j, 1) = green;
            image3(i, j, 2) = blue;
        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    int choose;
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    if (1 == choose) {
        image3.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> filename;
        image3.saveImage(filename);
        system(filename.c_str());
    }
}
void blur(string & filename){
    Image image4(filename);

    int blurRadius;
    cout << "Enter blur radius (odd number recommended): ";
    while (true) {
        cin >> blurRadius;
        if ( blurRadius >0 ) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    Image blurredImage = image4;

    for (int y = 0; y < image4.height; ++y) {
        for (int x = 0; x < image4.width; ++x) {
            int sumR = 0, sumG = 0, sumB = 0;

            for (int dy = -blurRadius / 2; dy <= blurRadius / 2; ++dy) {
                for (int dx = -blurRadius / 2; dx <= blurRadius / 2; ++dx) {
                    int nx = x + dx;
                    int ny = y + dy;

                    nx = max(0, min(nx, image4.width - 1));
                    ny = max(0, min(ny, image4.height - 1));

                    sumR += image4(nx, ny, 0);
                    sumG += image4(nx, ny, 1);
                    sumB += image4(nx, ny, 2);
                }
            }
            int avgR = sumR / (blurRadius * blurRadius);
            int avgG = sumG / (blurRadius * blurRadius);
            int avgB = sumB / (blurRadius * blurRadius);
            blurredImage(x, y, 0) = avgR;
            blurredImage(x, y, 1) = avgG;
            blurredImage(x, y, 2) = avgB;
        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    int choose;
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    if (1 == choose) {
        image4.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> filename;
        image4.saveImage(filename);
        system(filename.c_str());
    }
}
void Resize(string & filename){
    Image image5(filename);
    // the user enter the width and the height
    int Width, Height;
    cout << "Enter the width and height for the image: ";
    while (true) {
        cin >> Width >> Height;
        if ( Width > 0 && Height > 0) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }
    }

    // Create a resized image object with the new dimensions
    Image resizedImage(Width, Height);

    // Image resizing filter process //

    // Calculate the scaling factors for width and height
    double width_Scale = image5.width / (double) Width;
    double height_Scale = image5.height / (double) Height;

    // Loop for the pixels of the resized image
    for (int i = 0; i < Width; ++i) {
        for (int j = 0; j < Height; ++j) {
            for (int k = 0; k < image5.channels; ++k) {

                // Get the pixel value from the original image using linear interpolation and round it
                double scaledValue = round(image5.getPixel(i * width_Scale, j * height_Scale, k));

                // Set the rounded pixel value in the corresponding position of the resized image
                resizedImage.setPixel(i, j, k, static_cast<unsigned char>(scaledValue));
            }
        }
    }

    //  Save the resized image  //
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    int choose;
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    if (1 == choose) {
        image5.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> filename;
        image5.saveImage(filename);
        system(filename.c_str());
    }

}
void Crop(string &filename){
    //Read the image provided by the user
    Image userImage(filename);

    // the user enter the starting position for cropping
    int startX, startY;
    cout << "Enter the starting position (x, y) for cropping: ";
    while (true) {
        cin >> startX >> startY;
        if (startX > 0 &&  startY > 0) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }
    }

    //  the user enter the dimensions for cropping
    int width, height;
    cout << "Enter the height and the width of crop image: ";
    while (true) {
        cin >> width >> height;
        if ( width > 0 && height > 0) {
            break;
        } else {
            cout << "Invalid input. Please enter a number greater than zero " << endl;
            cin.clear();
            cin.ignore();
        }
    }

    // Create a new image with user-specified dimensions
    Image croppedImage(width, height);

    for (int i = 0; i < height; ++i) {
        for (int j = 0; j < width; ++j) {
            for (int k = 0; k < userImage.channels; ++k) {

                // Calculate the coordinates in the user's image for cropping
                int x = startX + j;
                int y = startY + i;

                // Check if the coordinates are within the bounds of the user's image
                if (x >= 0 && x < userImage.width && y >= 0 && y < userImage.height) {

                    // Set the pixel in the cropped image with the corresponding pixel from the user's image
                    croppedImage.setPixel(j, i, k, userImage.getPixel(x, y, k));
                }
            }
        }
    }
    int choise;
    cout << " choose 1 if you want to get cropped image with the same name of the image\n";
    cout << " choose 2 if you want to get cropped image with new name  \n";
    while (true) {
        cin >> choise;
        if ( choise == 1 || choise == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }

    if (choise == 1) {

        croppedImage.saveImage(filename);
        system(filename.c_str());


    } else if (choise == 2) {

        cout << "Please enter image name to store new image and specify extension (.jpg, .bmp, .png, .tga): ";
        cin >> filename;
        croppedImage.saveImage(filename);
        system(filename.c_str()); // Save the cropped image with the specified filename
    }
}
void Black_and_White(string &filename){
    Image image7(filename);

    for (int i = 0; i < image7.width; ++i) {
        for (int j = 0; j < image7.height; ++j) {

            unsigned int avg = 0;
            // Calculate the average color
            for (int k = 0; k < image7.channels; ++k) {
                avg += image7(i, j, k);
            }
            avg = avg / 3;
            // Set pixel to black or white
            for (int k = 0; k < 3; ++k) {
                if (avg < 128) {
                    image7(i, j, k) = 0;
                } else {
                    image7(i, j, k) = 255;
                }
            }
        }
    }
    cout << "Pls enter image name to store new image\n";
    cout << "and specify extension .jpg, .bmp, .png, .tga: ";

    cin >> filename;
    image7.saveImage(filename);
    system(filename.c_str());
}
void Flip(string& filename){
    cout << "choose 1 to flipped Horizontally :\n";
    cout << "choose 2 to flipped Vertical :\n";

    int choise;
    while (true) {
        cin >> choise;
        if ( choise == 1 || choise == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }

    // Flip the image horizontally
    if (choise == 1) {
        Image image8(filename);
        // Loop through half of the image width to perform horizontal flipping
        for (int i = 0; i < image8.width / 2; ++i) {
            for (int j = 0; j < image8.height; ++j) {
                for (int k = 0; k < image8.channels; ++k) {
                    // Swap the pixel values
                    swap(image8(i, j, k), image8(image8.width - 1 - i, j, k));
                }
            }
        }
        // Save the flipped image
        cout << "Pls enter image name to store new image\n";
        cout << "and specify extension .jpg, .bmp, .png, .tga: ";

        cin >> filename;
        image8.saveImage(filename);
        system(filename.c_str());
    }
        // Flip the image vertically
    else if (choise == 2) {
        Image image5(filename);
        for (int i = 0; i < image5.width; ++i) {
            // Loop through half of the height of the image to perform vertical flipping
            for (int j = 0; j < image5.height / 2; ++j) {
                for (int k = 0; k < image5.channels; ++k) {
                    // Swap the pixel values
                    swap(image5(i, j, k), image5(i, image5.height - 1 - j, k));
                }
            }
        }
        // Save the flipped image
        cout << "Pls enter image name to store new image\n";
        cout << "and specify extension .jpg, .bmp, .png, .tga: ";

        cin >> filename;
        image5.saveImage(filename);
        system(filename.c_str());


    }
}
void dark_and_bright(string & filename){
    string NImageNAme;
    int choose;

    Image image(filename);
    cout << "wanna bright the photo(1), wanna bright the photo(2)\n";
    while (true) {
        cin >> choose;
        if ( choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }
    }
    if (1 == choose) {
        for (int i = 0; i < image.width; ++i) {
            for (int j = 0; j < image.height; ++j) {
                for (int k = 0; k < 3; ++k) {
                    if ((image(i, j, k) + image(i, j, k) / 2) > 255) {
                        image(i, j, k) = 255;
                    } else if ((image(i, j, k) + image(i, j, k) / 2) <= 0) {
                        image(i, j, k) = 0;
                    } else {
                        image(i, j, k) = image(i, j, k) + image(i, j, k) / 2;
                    };
                }
            }
        }
    } else if (2 == choose) {
        for (int i = 0; i < image.width; ++i) {
            for (int j = 0; j < image.height; ++j) {
                for (int k = 0; k < 3; ++k) {
                    if ((image(i, j, k) - image(i, j, k) / 2) > 255) {
                        image(i, j, k) = 255;
                    } else if ((image(i, j, k) - image(i, j, k) / 2) <= 0) {
                        image(i, j, k) = 0;
                    } else {
                        image(i, j, k) = image(i, j, k) - image(i, j, k) / 2;
                    };
                }
            }
        }
    }

    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    while (true) {
        cin >> choose;
        if ( choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }}
    if (1 == choose) {
        image.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> NImageNAme;
        image.saveImage(NImageNAme);
        system(NImageNAme.c_str());
    }

    }
void merge(string & filename) {
    int choose;
    while (true) {
        cout << "merge only (1)\n";
        cout << "merge with resize(2)\n";
        cin >> choose;
        if (1 == choose || 2 == choose)break;

    }

    if (1 == choose) {
        string imgName2, NImageNAme;

        cout << "enter the second image name:\n";
        cin >> imgName2;


        Image image2(imgName2);
        Image image(filename);
        for (int i = 0; i < image.width; ++i) {
            for (int j = 0; j < image.height; ++j) {
                for (int k = 0; k < 3; ++k) {
                    image(i, j, k) = image(i, j, k) / 2 + image2(i, j, k) / 2;
                }
            }
        }
        cout << "enter the new image name\n";
        cin >> NImageNAme;
        image.saveImage(NImageNAme);
        system(NImageNAme.c_str());
    } else if (2 == choose) {
        string imgName2, NImageNAme;

        cout << "enter the second image name:\n";
        cin >> imgName2;


        Image image2(imgName2);
        Image image(filename);
        if (image.height != image2.height || image.width != image2.width) {
            // the user enter the width and the height
            int Width = image2.width, Height = image2.height;

            // Create a resized image object with the new dimensions
            Image resizedImage(Width, Height);

            // Image resizing filter process //

            // Calculate the scaling factors for width and height
            double width_Scale = image.width / (double) Width;
            double height_Scale = image.height / (double) Height;

            // Loop for the pixels of the resized image
            for (int i = 0; i < Width; ++i) {
                for (int j = 0; j < Height; ++j) {
                    for (int k = 0; k < image.channels; ++k) {

                        // Get the pixel value from the original image using linear interpolation and round it
                        double scaledValue = round(image.getPixel(i * width_Scale, j * height_Scale, k));

                        // Set the rounded pixel value in the corresponding position of the resized image
                        resizedImage.setPixel(i, j, k, static_cast<unsigned char>(scaledValue));
                    }
                }
            }

            //  Save the resized image  //
            resizedImage.saveImage(filename);
//crop filter
        }


        for (int i = 0; i < image.width; ++i) {
            for (int j = 0; j < image.height; ++j) {
                for (int k = 0; k < 3; ++k) {
                    image(i, j, k) = image(i, j, k) / 2 + image2(i, j, k) / 2;
                }
            }
        }
        cout << "enter the new image name\n";
        cin >> NImageNAme;
        image.saveImage(NImageNAme);
        system(NImageNAme.c_str());


    }
}
void greyscale(string & filename){
    string NImageNAme;
    int choose;


    Image image(filename);
    for (int i = 0; i < image.width; ++i) {
        for (int j = 0; j < image.height; ++j) {
            unsigned int avg = 0;
            for (int k = 0; k < 3; ++k) {
                avg += image(i, j, k);
            }
            avg = avg / 3;
            for (int k = 0; k < 3; ++k) {
                image(i, j, k) = avg;
            }
        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    if (1 == choose) {
        image.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> NImageNAme;
        image.saveImage(NImageNAme);
        system(NImageNAme.c_str());
    }}
void Edge(string & filename){
    string NImageName;
    cout << "input the new image name;\n";
    cin >> NImageName;

    Image image(filename);
//        Image Nimage("grydetect.jpg");
    for (int i = 0; i < image.width; ++i) {
        for (int j = 0; j < image.height; ++j) {
            unsigned int avg = 0;
            for (int k = 0; k < 3; ++k) {
                avg += image(i, j, k);
            }
            avg = avg / 3;
            for (int k = 0; k < 3; ++k) {
                image(i, j, k) = avg;
            }
        }
    }

    image.saveImage("graydetect.jpg");
    Image graydetect("graydetect.jpg");
//        Image  image_detect("new.jpg");
    Image edgeImage(graydetect.width, graydetect.height);

    EdgeDetection(graydetect, edgeImage);

    edgeImage.saveImage(NImageName);

    system(NImageName.c_str());
}
void infrared(string & filename){
    string NImageNAme;


    if (filename.empty()) {
        cerr << "Error: Could not open or find the image." << endl;
//        return -1;
    }
    Image image(filename);
    for (int i = 0; i < image.width; ++i) {
        for (int j = 0; j < image.height; ++j) {
            unsigned int avg = 0;
            for (int k = 0; k < 3; ++k) {
                avg += image(i, j, k);
            }
            avg = avg / 3;
            for (int k = 0; k < 3; ++k) {
                image(i, j, k) = avg;
            }
        }
    }


    for (int i = 0; i < image.width; ++i) {
        for (int j = 0; j < image.height; ++j) {

            image(i, j, 0) = 255;
            image(i, j, 1) = 255 - image(i, j, 1);
            image(i, j, 2) = 255 - image(i, j, 2);
        }
    }
    cout << "enter the new filename\n";
    cin >> filename;
    image.saveImage(filename);
    system(filename.c_str());
}
void Natural(string & filename){
    Image image11(filename);
    for (int i = 0; i < image11.width; ++i) {
        for (int j = 0; j < image11.height; ++j) {

            // Access the red, green, and blue channels of the current pixel
            unsigned char &red = image11(i, j, 0);
            unsigned char &green = image11(i, j, 1);
            unsigned char &blue = image11(i, j, 2);

            red *= 0.7;
            green *= 0.99;
            blue *= 0.8;

        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    int choose;
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    if (1 == choose) {
        image11.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> filename;
        image11.saveImage(filename);
        system(filename.c_str());
    }

}
void Purple(string & filename){
    Image image_purp(filename);
    int choose;
    string NImageName;
    for (int i = 0; i < image_purp.width; ++i) {
        for (int j = 0; j < image_purp.height; ++j) {
            image_purp(i, j, 1) *= 0.41;
        }
    }
    cout << "do you want save image with the same name(1)\n";
    cout << "want save image with new name(2)\n";
    while (true) {
        cin >> choose;
        if (choose == 1 || choose == 2) {
            break;
        } else {
            cout << "Invalid input. Please enter 1 or 2 : " << endl;
            cin.clear();
            cin.ignore();
        }

    }
    if (1 == choose) {
        image_purp.saveImage(filename);
        system(filename.c_str());
    } else if (2 == choose) {
        cout << "enter the new filename:\n";
        cin >> NImageName;
        image_purp.saveImage(NImageName);
        system(NImageName.c_str());
    }
}
int main() {
    string filename;
    while (true) {
        cout << " Welcome to this program for making filters\n ";
        cout << "Enter the filename of the image to Apply the filter on :\n ";
        cin >> filename;
        if (filename.empty()) {
            cout << "Error: Could not open or find the image . Please enter a valid filename." << endl;
        } else {
            break;
        }
    }
    while (true) {

        cout << "Which filter do you want to use?" << endl;
        cout << "Main filters" << endl;
        cout << "1- Invert Image" << endl;
        cout << "2- Rotate Image" << endl;
        cout << "3- Frame Image" << endl;
        cout << "4- Blur image" << endl;
        cout << "5- Resize image" << endl;
        cout << "6- Crop image" << endl;
        cout << "7- Black and White image" << endl;
        cout << "8- Flip Image" << endl;
        cout << "9- Dark and bright image" << endl;
        cout << "10- Merge image" << endl;
        cout << "11- Greyscale image" << endl;
        cout << "12- Edge detect image" << endl;
        cout << "Bonus filters" << endl;
        cout << "13- Infrared filter" << endl;
        cout << "14- Natural Sunlight Filter" << endl;
        cout << "15- Purple Filter" << endl;
        cout << "16- exit the program" << endl;
        cout << "Enter your choice:-";
        int choice;

        while (true) {
            cin >> choice;
            if (choice >= 1 && choice <= 16) {
                break;
            } else {
                cout << "Invalid input. Please enter a number from 1 to 16 " << endl;
                cin.clear();
                cin.ignore();
            }
        }
        if (choice == 1) {

            Invert(filename);
        }
            //rotate image
        else if (choice == 2) {
            Rotate(filename);
        }
            //framed filter
        else if (choice == 3) {
            framed(filename);

        }
            //blur filter
        else if (choice == 4) {
            blur(filename);
        } else if (choice == 5) {
            Resize(filename);
        }
            //crop filter
        else if (choice == 6) {
            Crop(filename);
        }
            // Black and White Filter
        else if (choice == 7) {
            Black_and_White(filename);
        } else if (choice == 8) {
            Flip(filename);
            // Flip Image Filter
        }
            //filter:dark and bright
        else if (choice == 9) {
            dark_and_bright(filename);
        }

            //filter:merge
        else if (choice == 10) {
            merge(filename);
        }

            //filter:greyscale
        else if (choice == 11) {
            greyscale(filename);
        } else if (choice == 12) {
            Edge(filename);
        }
            //infrared filter
        else if (choice == 13) {
            infrared(filename);
        }
            // The Process of Natural Sunlight Filter
        else if (choice == 14) {
            Natural(filename);
        } else if (choice == 15) {
            Purple(filename);
        }
            //exit the program
        else if (choice == 16) {
            break;
            exit(0);
        }

        cout << "Do you want to apply another filter ( 1 for Yes , 0 for No ) : \n ";
        int choise;
        while (true) {

            if (choise == 0) {
                cout << "End of the program";
                break;

            } else if (choise == 1) {
                if (filename.empty()) {
                    cout << "Error: Could not open or find the image, pls ";
                } else break;

            }
        }
    }



    return 0;
}
