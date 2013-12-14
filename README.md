File-uploads-and-validation
===========================

Uploading files and validating the extensions


/* Check if a file has been uploaded or not */
if ( is_uploaded_file ( $_FILES['file_name']['tmp_name'] )) {

  /* Array of allowed extensions 
  'application/msword' - validates DOC documents
  'application/vnd.openxmlformats-officedocument.wordprocessingml.document' - This long line validates DOCX documents
*/
  $allowed = array ( 'application/pdf', 'application/x-pdf', 'text/pdf', 'text/x-pdf', 'application/vnd.openxmlformats-officedocument.wordprocessingml.document', 'application/msword' );

  /* Check if the uploaded file's extension is in $allowed array */
  if ( in_array ( $_FILES['file_name']['type'],$allowed )) {

    /* Getting the extension of uploaded document */
    $ext = pathinfo ( $_FILES['file_name']['name'], PATHINFO_EXTENSION );

    /* renaming the uploaded document as per requirement */
    $file_name = 'desiredFilename.'.$ext;
    $temp = './desiredLocation/'.$file_name;

    /* Check if that file was moved to the desired location */
    if ( move_uploaded_file ( $_FILES['file_name']['tmp_name'], $temp)) {
      $success = 'File uploading successful!!';
    } else {
      $errors = 'The file could not be moved.';
    } // End of if(move_uploaded_file($_FILES[.........

  } else {
    $errors = 'Invalid format . Please select a pdf, x-pdf, docx or doc file only.';

  } // End of if(in_array($_FILES[..........
} // End of main if ( is_uploaded_file
