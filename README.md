# Image-processing
counting the number of coins in a image using matlab

mg = imread('coins.png');               % Read image

% Check if image is already grayscale

if size(img, 3) == 3                      % RGB image
  
    gray_img = rgb2gray(img);  
else                                       % Already grayscale
   
    gray_img = img;  
end


bw = imbinarize(gray_img);                % Binarize the image

bw = imfill(bw, 'holes');  

               % Fill holes inside the coins

% Apply morphological operations to remove noise

se = strel('disk', 15);                   % Structuring element (adjust size)

bw_clean = imopen(bw, se);                % Remove small noise

bw_clean = bwareaopen(bw_clean, 500);     % Remove very small regions

% Count connected components

stats = regionprops(bw_clean, 'Area');    % Detect regions

num_coins = numel(stats);                 % Count the regions

imshow(bw_clean);                         % Display cleaned image

title(['Number of Coins: ', num2str(num_coins)]);

disp(['Number of coins: ', num2str(num_coins)]);

Result
![Screenshot 2025-03-29 174321](https://github.com/user-attachments/assets/2b851244-5ef9-40b2-98ba-46f73293da37)
![Screenshot 2025-03-29 174356](https://github.com/user-attachments/assets/8bb3506f-b9f4-4002-93c4-74fa1d0a2998)




