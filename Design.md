# task_note Design

## Program Flow

#. Read the task ID for which note should be created or read
#. Get the UUID for the task ID
#. Generate NOTEFILE name
#. Create TEMPFILE with name UUID contained within
#. Does NOTEFILE exist?
	#. Yes
		#. vim NOTEFILE
		#. Is NOTEFILE newer than TEMPFILE?
			#. Yes
				#. task N ann "Notes updated"
	#. No
		#. vim -c ":0r TEMPFILE" NOTEFILE
		#. Does NOTEFILE exist?
			#. Yes
				#. task N ann "Note Location: NOTEFILE"
#. Delete TEMPFILE

