Holds the content of the [Kayak Cincinnati][kc] website

Depolys are done via a rake task that runs a ruby script that uses Net:SFTP.
The xferlist.rb script can be found at <https://gist.github.com/997254>

After making changes:

* run `rake`
* git add the changed files including the sentinel* files  
  you probably have to `git add -f sentinel*`
* git push

[kc]: http://kayakcincinnati.com/ "Kayak Cincinnati"
