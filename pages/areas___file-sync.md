- one way vs two ways
- common features:
	- [Encryption](https://en.wikipedia.org/wiki/Encryption) for [security](https://en.wikipedia.org/wiki/Internet_security), especially when synchronizing across the [Internet](https://en.wikipedia.org/wiki/Internet).
	- [Compressing](https://en.wikipedia.org/wiki/Data_compression) any data sent across a network.
	- *Conflict detection* where a file has been modified on both sources, as opposed to where it has only been modified on one. Undetected conflicts can lead to overwriting copies of the file with the most recent version, causing data loss. For conflict detection, the synchronization software needs to keep a database of the synchronized files. Distributed conflict detection can be achieved by [version vectors](https://en.wikipedia.org/wiki/Version_vector).
	- *Open Files Support* ensures data integrity when copying data or application files that are in-use or database files that are exclusively [locked](https://en.wikipedia.org/wiki/File_locking).
	- Specific support for using an intermediate storage device, such as a removable flash disc, to synchronize two machines. Most synchronizing programs can be used in this way, but providing specific support for this can reduce the amount of data stored on a device.
	- The ability to preview any changes before they are made.
	- The ability to view differences in individual files.
	- Backup between operating systems and transfer between network computers.
	- Ability to edit or use files on multiple computers or operating systems.