- how to add bookmarks in linux
	- use [Document Viewer](https://en.wikipedia.org/wiki/Evince) to add bookmarks
	- create bookmarks.txt, copy BookmarkTitle and BookmarkPageNumber from Document Viewer
		- ```
		  BookmarkBegin
		  BookmarkTitle: PDF Reference (Version 1.5)
		  BookmarkLevel: 1
		  BookmarkPageNumber: 1
		  BookmarkBegin
		  BookmarkTitle: Contents
		  BookmarkLevel: 2
		  BookmarkPageNumber: 3
		  ```
	- ``` bash
	  pdftk sample.pdf \
	  update_info bookmarks.txt \
	  output sample_bookmarked.pdf
	  ```