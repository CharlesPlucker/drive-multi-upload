Upload multiple large files to Google Drive using Google Apps Script
<a name="top"></a>
=====

<a name="overview"></a>
# Overview
This is a sample form that will take a folder name, create that folder under a hardcoded parent folder, and upload 1 or more large files (> 50 MB). The form uses Google Apps Script (GAS), in order to interface with google drive's api.

<a name="description"></a>
# Description
This form came from a need to provide an easy way for someone to upload large files to google drive via a simple interface accessible on any device. Originally I was creating files using the Google Drive DriveApp api but quickly realized that uploading larger files was not supported. It looked like the resumable upload option is what I wanted. I found some closely linked resources, but those examples would only upload one file at a time. This solution will upload multiple files sequentially and put them in a new folder in the provided parent folder. The code uses the Google Drive DriveApp api to get an oAuth token, and to create the folders in the right place. Here are the general steps of the code:

1. Validate the form
2. One file at a time, load the file into the browser
3. Using the hardcoded `uploadParentFolderId` Id, find that folder
4. As a child of this folder check if a folder with the name you entered exists. If it exists the code reuses that folder. If it doesn't already exist it creates a new folder with that name
5. Divide the file up into chunks that can be sent one at a time to the server. Update the % updated display with progress
6. Once successful, move to next file

<a name="getting-started"></a>
# Getting Started
This form is made up of two files: `forms.html`, and `Code.gs`. Follow these steps to run them:
1. Go to http://script.google.com
2. Click on "New Script" at the top left of the page
3. Paste the contents of `Code.gs` into the `Code.gs` file that opens up
4. Click "File" -> "New" -> "HTML file" and name it forms.html
5. Copy the contents of `forms.html` into the newly created `forms.html`
6. Deploy your code by going to "Publish" -> "Deploy as web app..."
7. Leave the defaults or modify them as you please
8. Authorize the app by Reviewing Permissions and allowing this script to modify your google drive. (If you see a "BACK TO SAFETY" button you should click "Advanced", then the link that says "unsafe")
9. Click on the "latest code" link to view the form. (you can always find this link again by going to "Publish" -> "Deploy as web app..." and clicking on the "latest code" link there)



<a name="future-work"></a>
# Future Work
- When creating a new folder, if you try to fetch that folder immediately afterwards, it can fail and not return the proper response. In my testing this hasn't been an issue but I'd like for that api to be more robust. Perhaps poll until a better response is received.
- Team Drive support. I would like to upload these files to a folder in a shared drive

<a name="acknowledgements"></a>
# Acknowledgements
This form was mostly put together from work found in the following resources:
- https://raw.githubusercontent.com/tanaikech/Resumable_Upload_For_WebApps
