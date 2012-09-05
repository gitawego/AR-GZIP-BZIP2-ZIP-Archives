AR-GZIP-BZIP2-ZIP-Archives
==========================

A tar, gzip, bzip2, and zip archives manager

forked from http://www.phpclasses.org/package/945-PHP-Create-tar-gzip-bzip2-zip-extract-tar-gzip-bzip2-.html

TAR/GZIP/BZIP2/ZIP ARCHIVE CLASSES Examples

Examples of Compression:

The following example creates a gzipped tar file:

    // Assume the following script is executing in /var/www/htdocs/test
    // Create a new gzip file test.tgz in htdocs/test
    $test = new gzip_file("htdocs/test/test.tgz");
    // Set basedir to "../..", which translates to /var/www
    // Overwrite /var/www/htdocs/test/test.tgz if it already exists
    // Set compression level to 1 (lowest)
    $test->set_options(array('basedir' => "../..", 'overwrite' => 1, 'level' => 1));
    // Add entire htdocs directory and all subdirectories
    // Add all php files in htsdocs and its subdirectories
    $test->add_files(array("htdocs", "htsdocs/*.php"));
    // Exclude all jpg files in htdocs and its subdirectories
    $test->exclude_files("htdocs/*.jpg");
    // Create /var/www/htdocs/test/test.tgz
    $test->create_archive();
    // Check for errors (you can check for errors at any point)
    if (count($test->errors) > 0)
      print ("Errors occurred."); // Process errors here


The following example creates a zip file:

    // Create new zip file in the directory below the current one
    $test = new zip_file("../example.zip");
    // All files added will be relative to the directory in which the script is 
    //    executing since no basedir is set.
    // Create archive in memory
    // Do not recurse through subdirectories
    // Do not store file paths in archive
    $test->set_options(array('inmemory' => 1, 'recurse' => 0, 'storepaths' => 0));
    // Add lib/archive.php to archive
    $test->add_files("src/archive.php");
    // Add all jpegs and gifs in the images directory to archive
    $test->add_files(array("images/*.jp*g", "images/*.gif"));
    // Store all exe files in bin without compression
    $test->store_files("bin/*.exe");
    // Create archive in memory
    $test->create_archive();
    // Send archive to user for download
    $test->download_file();



Examples of Decompression:

The following example extracts a bzipped tar file:

    // Open test.tbz2
    $test = new bzip_file("test.tbz2");
    // Overwrite existing files
    $test->set_options(array('overwrite' => 1));
    // Extract contents of archive to disk
    $test->extract_files();
    
    The following example extracts a tar file:
    // Open archives/test.tar
    $test = new tar_file("archives/test.tar");
    // Extract in memory
    $test->set_options(array('inmemory' => 1));
    // Extract archive to memory
    $test->extract_files();
    // Write out the name and size of each file extracted
    foreach ($test->files as $file)
    	print ("File " + $file['name'] + " is " + $file['stat'][7] + " bytes\n");
