# research-into-serverless-git-based-cms
	
i have been asked by a small music venue to see if i could simplify their drupal install
since i dont know php, and since the website is mostly just a bunch of bloglike posts with events, i thought it would make a good candidate for a static page

THAT is until i figured out the backcatalog of posts going back to 2011 with huge image assets.

so i came up with this plan: https://github.com/sloev/research-into-serverless-git-based-cms/blob/main/README.md

which roughly is to create two repos: one repo for a single file cms in the form of a cloudflare worker that does ultra simple access control together with image upload (presigned backblaze urls) and form submit (musicevents new/updated) as json

another repo for keeping the layout plus all the music events json etc this repo can be public andwill build static html on each push

my question is : "is this gonna make the site more maintainable in the future?"

currently they have no person responsible for the website s it has to be easy to get into and maintain for an occational dev

goal:

1. browser based cms system that is focussed on "posts" 
    1. posts are entries of similar layout
    2. posts can be draft or edits
    3. posts have metadata (tags, author, dates) connected to them 
    4. posts have content that is "rich text" but really is strict json
    5. posts **can have images**
    6. posts and their content are autosaved to github using the api
  
3. a hugo or other static site generator uses the posts plus a layout to generate static html
4. to be able to upload images:
    1. a service needs to be able to upload images to backblaze
    2. a service needs to be able to transform images
    3. client side image compression: https://davidmoodie.com/client-compress/
    4. a service has to first get a presigned url for a backblaze upload (https://github.com/mattwelke/upload-file-to-backblaze-b2-from-browser-example) and then post the image to that url
5. two repo's are created, one for the page (can be public) one for the cms (has to be closed)
6. a serverless function has is responsible for user access, image upload and post editing
    1. it will live in the cms repo
    2. the cms repo is private and has the users info in it with passwords (https://security.stackexchange.com/questions/211/how-to-securely-hash-passwords)
    3. the cms repo will be updated when users edit it in the cms
7. the cms page will use editor.js
