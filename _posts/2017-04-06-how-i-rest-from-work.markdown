---
layout: post
title: How I Rest From Work
date: 2017-09-12 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Holidays, Hawaii]
---
#1. Your own Marketing Automation System - The Basics

Did you know that you could use Google Sheet as the basis for your very own Marketing Automation system? I bet you didn’t. 

Prerequisites:
- Gmail account. You can use your personal account, but you will be limited in the amount of mails you can send. 
- Emails put in your sheet. See this tutorial to learn more

**Goal: Create personalized emails that are being sent on specific triggers.**

##Create a new sheet
Copy [this sheet]. It contains the following fields: 

(img)

Fill in your email address, name and the subject for a test mail.

##Activate the script
Go to Tools -> Script editor. You can see the following script:
 
// This constant is written in column D for rows for which an email has been sent successfully.
var EMAIL_SENT = 'EMAIL_SENT';

/**
 * Sends non-duplicate emails with data from the current spreadsheet.
 */
function sendEmails2() {
  var sheet = SpreadsheetApp.getActiveSheet();   
  
  var startRow = 1; // First row of data to process
  var dataRange = sheet.getDataRange();
  // Fetch values for each row in the Range.
  var data = dataRange.getValues();
  for (var i = 1; i < data.length; ++i) {
	var row = data[i];
	var emailAddress = row[0]; // First column
	var name = row[1]; // Second column
	var subject = row[2]; // Third column
	var emailSent = row[3]; // Fourth column
	
	var htmlBody = "<html> <body> <h1>Hi " + name +"</h1> <p>My first paragraph.</p> </body> </html>"

	
	if (emailSent != EMAIL_SENT) { // Prevents sending duplicates

	MailApp.sendEmail({
		to: emailAddress,
		subject: subject,
		htmlBody: htmlBody,
  });      
	  
	  sheet.getRange(startRow + i, 4).setValue(EMAIL_SENT);
	  // Make sure the cell is updated right away in case the script is interrupted
	  SpreadsheetApp.flush();
	}
  }
}


##Personalized body

[https://developers.google.com/apps-script/articles/mail\_merge]


##Run the script and grant permission
Click on Run and give the script permission to send emails. 

##Check your mail
If all is well, you have just received your very first email.




Script:
[https://www.youtube.com/watch?v=3dGQ4d7JF1U&t=1365s&list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw&index=14]

Add HTML body:
[https://productforums.google.com/forum/#!topic/docs/Us8SRAVr6YU]

[https://chrome.google.com/webstore/detail/mail-merge-with-attachmen/nifmcbjailaccmombpjjpijjbfoicppp]

