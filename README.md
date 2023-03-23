# research-into-serverless-git-based-cms

goal:
1. browser based cms system that is focussed on "posts" 
  a. posts are entries of similar layout
  b. posts can be draft or edits
  c. posts have metadata (tags, author, dates) connected to them 
  d. posts have content that is "rich text" but really is strict json
  e. posts **can have images**
  f. posts and their content are autosaved to github using the api
  
3. a hugo or other static site generator uses the posts plus a layout to generate static html
4. to be able to upload images:
  a. a service needs to be able to upload images to backblaze
  b. a service needs to be able to transform images
  c. client side image compression: https://davidmoodie.com/client-compress/
  d. a service has to first get a presigned url for a backblaze upload (https://github.com/mattwelke/upload-file-to-backblaze-b2-from-browser-example) and then post the image to that url
5. two repo's are created, one for the page (can be public) one for the cms (has to be closed)
6. a serverless function has is responsible for user access, image upload and post editing
  a. it will live in the cms repo
  b. the cms repo is private and has the users info in it with passwords (https://security.stackexchange.com/questions/211/how-to-securely-hash-passwords)
  c. the cms repo will be updated when users edit it in the cms
7. the cms page will use editor.js
