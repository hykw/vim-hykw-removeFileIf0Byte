vim-hykw-removeFileIf0Byte
==========================

When you save the file, if the filesize is 0 byte, it confirm to REMOVE the file(also close the buffer)

It's too small snippets, I writes it in .vim file like below.
When you answer y, it just removes both the file and buffer.

    augroup hykw_removeFile
      autocmd!
      autocmd BufWritePost * call s:Hykw_removeFileIf0Byte()
    augroup END
    
    function! s:Hykw_removeFileIf0Byte()
      let filename = expand('%:p')
      let bufname = expand('%:t')
      if getfsize(filename) > 0
        " do nothing
        return
      endif
    
      let msg = printf("\n%s is empty, remove?(y/N)", filename)
      if input(msg) == 'y'
        call delete(filename)
        bdelete
      endif
    endfunction
