---
layout: 'post'
title: 'How To Move Users From Joomla To WordPress'
date: 2017-10-06
author: 'Chad Warford'
excerpt: 'Log Into Your WordPress Website With Your Joomla Credentials'
twitter: 'https://twitter.com/warforddesigns'
github: 'https://github.com/DigitalDesignerOnline/'
website: 'https://digitaldesigneronline.com'
---

While working on a recent Client project, I was requested to rebuild their current Joomla CMS website into a WordPress CMS website. The Client heard about the user friendly interface of WordPress and after testing out its functionality instantly fell in love. Another issue they had was that the originally developed website was so out of date it could not even be updated without crashing the entire website. This unfortunatly was not an option. You see the website in question was accessed daily by over 2000 members for work purposes. This means no website, no work for that day. As the current website was at a very outdated state there were also security vulnerabilities to take into consideration as well.

The client didn’t want their members to have to re-register with the new site and requested for our team to implement a solution which would allow the members to both keep their account but also their current password in order to be able to seamlessly log into their new members portal.

After many cups of coffee, and numerous more hours of researching, it was clear that this was a very sought after process with many vague and unsuccessful results. Until I came across a article on bhoover.com which led me to a couple choice plugins, one which has been updated recently by a WordPress community contributor thankfully.

Step 1 - Export Joomla Users Database Table

The first step in moving the Clients Joomla Users to the new WordPress site was as simple as logging into phpmyadmin where your Joomla websites database is located. select the joomla users database table and export the table to a csv file.

When pulling the data from your mySQL database be sure to pull a minimum of the following columns:
name, username, email, password and registered date.

You will also want to seperate the name column into two seperate columns for first and last name however we will be addressing this in a later step.

Thats it, as easy as that we now have our entire user list in a nice easy to use csv file which we can now open in our favorite spreadsheet editor such as Microsoft Excel or OpenOffice Calc for an example.

Step 2
Prepare Database for WordPress

There are a few quick steps we need to undertake prior to importing our csv file to the WordPress database. Here are the steps involved:

1. Update table column names to coincide with the WordPress table structure
2. Separate Name into First and Last name columns.
3. Remove any unwanted and unnecessary table columns.
4. Rearrange certain columns to work with the import plugin we will be using.
1. First we are going to update the column names to ensure they follow the WordPress table structure. To do this we will simply open the csv file into our spreadsheet editor and change the following table columns to their new names and arrangement as follows; 

NOTE: The Password column MUST be titled “joomlapass”.

As you can see we have also separated the name into first and last name columns. To do this simply follow these easy steps and removed any unwanted columns of data.
i. Begin by selecting the entire name column by clicking the number above, you will know you have the whole column selected as the entire column will be highlighted.
ii. Within the Data menu select Text to Column. Choose the option for Delimited and set the character to split as a <strong>Space</strong>.

Once done click Finish. If your data did not correctly separate into two columns you can simply press CTRL-Z on your keyboard to undo the step and try again making the necessary adjustments.

Step 3
Import Joomla User CSV File to WordPress Database

Once we have made these few minor modifications its time to log into the new wordpress website and add our plugin. For this we will be using <a href="http://wordpress.org/extend/plugins/import-users-from-csv/" target="_blank">"Import Users From CSV"</a>.
Once installed navigate in your Dashboard to Tools > Import users from CSV and edit the settings to your desired member setup. Upload your csv file and select Start Importing. To verify that the process completed correctly visit your Users tab within the Dashboard to see all your newly added users populated.

Step 4
Integrate Joomla User Authentication to WordPress

In order to accomplish this task we will be utilizing the "Joomla to WP Migrated Users Authentication Plugin" which is a modified and updated version of the original within the WordPress repository.
Here is how it works:

"When the user logs in the first time after migration, his/her password is hashed using the Joomla method (either md5:salt or PHPass) and compared with value in joomlapass meta key. If the password is correct, the WordPress user is updated and the password encrypted to the WordPress password format and stored in the user_pass field. For all subsequent logins, the user will now be authenticated via the standard WordPress authentication plugin. At this time, the joomlapass meta key is renamed to joomlapassbak to avoid repeatedly performing this conversion.”
basically, this plugin will intercept the login process, verify if the Joomla password is correct for the user, if it is it will then create a WordPress password and bypass the joomla process for all future login attempts.

There you have it! We are all done. You should now be able to log into your WordPress website with your Joomla credentials. The best part your members will not have to re-register to your website.
