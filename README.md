### Hubot Webserver
--------------------

This repository contains the naive, mundane, highly interesting, but poorly created code for http://macros.ealui.com/

The purpose of the subdomain is currently to display all the usable macros in the hipchat server belonging to the one and only Llama Tom's and Friends. It is built specifically for the needs of us - and therefore, this project is probably of no use to those who are not part of our hipchat ):

### How to use
---------------

The webserver is built on a set of static auto-generated HTML pages. We have a simple cron job that runs daily to generate the html pages to display all the macros at once. The two key files in this repository are the macro_html_gen.py file and the www/index.html page.

In order to keep things simple, we rely on AJAX calls to load each auto-generated html page, thus the reason why we really only care about index.html ---- all the javascript, and fancy smanshy UI code can be found in this single file. Do note however, that were is auto-generated code in this file as well. That code is specifically the pagination elements <li> items near the bottom. This is because we do not know how many pages there are, so we dynamically calculate and insert the elements.

To test this code, you will need a copy of our db -> dump.rdb -> which can be found in https://github.com/ericluii/hubot - which is backed up daily. To all you folks sniffing for evil things to do... there really is nothing evil you can do with our db... we don't store secrets on it.

Once you have a copy of this file, you will need rdbtools and BeautifulSoup.

rdbtools is for parsing the dump file, and outputting it in a json form with the following command:

  rdb --command json dump.rdb > db.json
  
BeautifulSoup is a python module used for modifying and creating HTML code easily (:
So all together, we have the following steps

1. Install rdbtools(sudo pip install rdbtools) and install BeautifulSoup(sudo pip install BeautifulSoup)
2. Create your json blob with the command above(rdb --command json dump.rdb > db.json)
3. Place sed json blob in the root folder of this repository
4. Run the script!(python macro_html_gen.py)
Note: You may need to create a folder called 'gen' in the 'www' folder

You will now have all the beautifully generated html files :D
Now you can pick your favourite HTTP Server and run it in the www folder and you will have our beautiful macros page (:
For example, if you use python, this might work for you(python -m SimpleHTTPServer 8000) In which case, just point your browser to http://localhost:8000 <- and you are golden :3
