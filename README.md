from PIL import Image
import numpy as np

def encrypt_image(image_path, output_path, key):
    image = Image.open(image_path)
    pixels = np.array(image)
    encrypted_pixels = (pixels + key) % 256
    encrypted_image = Image.fromarray(encrypted_pixels.astype('uint8'))
    encrypted_image.save(output_path)
    print(f"Image encrypted and saved to {output_path}")

def decrypt_image(image_path, output_path, key):
    image = Image.open(image_path)
    pixels = np.array(image)
    decrypted_pixels = (pixels - key) % 256
    decrypted_image = Image.fromarray(decrypted_pixels.astype('uint8'))
    decrypted_image.save(output_path)
    print(f"Image decrypted and saved to {output_path}")

def swap_pixels(image_path, output_path, key):
    image = Image.open(image_path)
    pixels = np.array(image)
    np.random.seed(key)
    indices = np.arange(pixels.size)
    np.random.shuffle(indices)
    swapped_pixels = pixels.flatten()[indices].reshape(pixels.shape)
    swapped_image = Image.fromarray(swapped_pixels.astype('uint8'))
    swapped_image.save(output_path)
    print(f"Image pixel-swapped and saved to {output_path}")

def main():
    print("Image Encryption Tool")
    choice = input("Do you want to (e)ncrypt, (d)ecrypt, or (s)wap pixels? ")
    image_path = input("Enter the path to the input image: ")
    output_path = input("Enter the path to save the output image: ")
    key = int(input("Enter an encryption key (integer): "))

    if choice.lower() == 'e':
        encrypt_image(image_path, output_path, key)
    elif choice.lower() == 'd':
        decrypt_image(image_path, output_path, key)
    elif choice.lower() == 's':
        swap_pixels(image_path, output_path, key)
    else:
        print("Invalid choice! Please choose 'e' for encrypt, 'd' for decrypt, or 's' for swap pixels.")

if __name__ == "__main__":
    main()
