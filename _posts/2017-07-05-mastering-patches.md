Patches

07/08/14
How to read a patch
Hunks
Then follow sets of changes, called hunks. Each hunk starts with a line that contains, 

1. enclosed in@@, showing the context start line, 

2. no-of-lines in the file before (with a -) and after (with a +) the changes. After that come the lines from the file. Lines starting with a - are deleted, lines starting with a + are added. Each line modified by the patch is surrounded withbefore and after.

An addition looks like this:

@@ -75,6 +77,8 @@
 foo
 bar
 baz
+line1
+linemore
 and still context
That means, in the original file after line 78 (= 75 + add . These will be lines 80 (= 77 + through.
A deletion looks like this:
@@ -75,7 +75,6 @@
 foo
 bar
 baz
-linemore
 and still context
That means, delete line 78 (= 75 + in the original file. The unchanged context will be on lines.
Finally, a change looks like this:
@@ -70,7 +70,7 @@
 foo
 bar
 baz
-red
+blue
 more context
 and more
 still context
That means, change line 73 (= 70 + in the file before all changes, which contains red to blue. The changed line is also line 73 (= 70 + in the file after all changes.



Windows vs Unix file format

I suspect that this error is more related with the fileformat that with the pach offset.
We have been able to apply the patch doing the following:

$ vi configure_links-1277444-1.patch

:set ff=unix <enter>
:wq! <enter>

Once the file format is changed and we are again in the prompt:

$ patch -p1 < configure_links-1277444-1.patch
patching file content_lock.info
Hunk #1 succeeded at 14 (offset 3 lines).
patching file modules/content_lock_timeout/content_lock_timeout.info
Hunk #1 succeeded at 8 (offset 3 lines).

Then I checked manually and the files were been pached correctly. 
Did you already tried this? Please let us know if this work also for you.


If you add a new file:

--- /dev/null
+++ sites/all/modules/contributed/eu_cookie_compliance/js/eu_cookie_compliance.admin.js

Applying patches with patch

To apply a patch to a single file, change to the directory where the file is located and call patch:

patch < foo.patch

These instructions assume the patch is distributed in unified format, which identifies the file the patch should be applied to. If not, you can specify the file on the command line:

patch foo.txt < bar.patch

The -p level 
When file to be patched and patch are in different folders you have to be careful about setting a "p level". 
The p level instructs patch to ignore parts of the path name so that it can identify the files correctly. 

patch -p1 < baz.patch

You should change to the top level source directory before running this command. 
If a patch level of one does not correctly identify any files to patch, inspect the patch file for file names. 

Example #1
Patch is to be found in sites/all/modules/contributed/date , while file to be patch is sites/all/modules/contributed/date/date_views/includes/date_views_filter_handler_simple.inc

2 level deeper.

In this case you run


/sites/all/modules/contributed/date $ patch -p1 -R < 1876168-47-exposed_date_filter_groups.patch
patching file date_views/includes/date_views_filter_handler_simple.inc



Example #2

If you file to be patch is /users/stephen/package/src/net/http.c  and you are working in a directory that contains net/http.c, use

patch -p5 < baz.patch
In general, count up one for each path separator (slash character) that you remove from the beginning of the path, until what's left is a path that exists in your working directory. The count you reach is the p level.

To revert patch, 

use the -R flag, ie
patch -p5 -R < baz.patch
or git apply -R path/file.patch 

Patches can be undone, or reversed, with the '-R' option:
$ patch -R < /path/to/file 

Apply patch to multiple files:
host # patch -p0 -i patchfile.patch
patching file tmpdir1/file1
patching file tmpdir1/file2
Creating patches with diff

with single files, 
To create a patch for a single file, use the form:

diff -u original.c new.c > original.patch

-u option will generate the context
or entire source directories. 
1. make a copy of the tree:

cp -R original new

Make any changes required in the directory new/. Then create a patch with the following command:

diff -rupN original/ new/ > original.patch

This generates a  unified multifile patch

That's all you need to get started with diff and patch. For more information use:

man diff
man patch
Diff and colordiff

Generate a patch using diff command:
diff -c tmpdir1 tmpdir2  >patchfile.patch
cat patchfile.patch
If you prefer to use a terminal, colordiff (in the colordiff package) provides syntax highlighting. If the patch is long, you may want to use less to look at it. 

Patch naming convention

Adhere to Drupal patch naming convention:
[issue_name][short-description][issue-number]-[comment-number]

e.g: media-indexOf-IE-2108647-4.patch

Why:
On module update some patches become obsolete. This facilitate their removal
As for now is impossible or hard to guess what each patch is doing. After adheretion you may easily find the drupal.org page with the patch description // simpletest pass status // new version and improvements

So the convention would be to stick to Drupal convention for Drupal.org pathces and stick to JIRA ticket number for our own patches. 


Other options
-b – keep a file backup
Upon startup patch command try to figure out the type of diff listing unless overriden by -c (context), -e, -n, or -u (unified).

The names of the files to be patched are usually taken from the patch file, but if there's just one file to be patched it can specified on the command line as originalfile

References
http://www.markusbe.com/2009/12/how-to-read-a-patch-or-diff-and-understand-its-structure-to-apply-it-manual