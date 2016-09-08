---
layout: post
title:  "Getting started with Backup gem"
date:   2016-09-05 16:15:00
categories: Development Ruby on Rails PostgreSQL pg_dump Backup
---
I've been following [this great tutorial](http://vladigleba.com/blog/2014/06/30/backup-a-rails-database-with-the-backup-and-whenever-gems/) to set up the pretty useful [Backup gem](https://github.com/backup/backup), which can be used to... surprise! Backup your database.

Instead of using SCP, as the original author did, I'm just creating the backup in my local computer. I'm planning to use Dropbox in a future post. So, this was way simpler, but I had some little problems, so I'm writing this small post as a reminder.

The steps I followed are these:

1.  Install the gem

        juan@ubuntu:~/seven$ gem install backup

2. Run the `backup generate:model` command, to create the model and config file

        juan@ubuntu:~/seven$ backup generate:model --trigger=db_backup --databases='postgresql' --storages='local' --compressor='gzip' --notifiers='mail'

    We should see this output:

        Generated configuration file: '/home/juan/Backup/config.rb'.
        Generated model file: '/home/juan/Backup/models/db_backup.rb'.

    We're editing only the model file, although we could move some general config (like the mail credentials) to the config file.

3. Edit the model

        juan@ubuntu:~/seven$ subl ~/Backup/models/db_backup.rb 

    and set whatever needed values, like:

        db.name               = "seven_development"
        db.username           = "juan"
        db.password           = "juan"

4. Also, in this file, set the tables to be skipped

        db.skip_tables        = ["public.ar_internal_metadata"]

5. And the mail settings, too

        notify_by Mail do |mail|
            mail.on_success           = true
            mail.on_warning           = true
            mail.on_failure           = true
        
            mail.from                 = "mailer.daemon.seven@gmail.com"
            mail.to                   = "mailer.daemon.seven@gmail.com"
            #mail.cc                   = "cc@email.com"
            #mail.bcc                  = "bcc@email.com"
            #mail.reply_to             = "reply_to@email.com"
            mail.address              = "smtp.gmail.com"
            mail.port                 = 587
            #mail.domain               = "your.host.name"
            mail.user_name            = "mailer.daemon.seven@gmail.com"
            mail.password             = "MyPass"
            mail.authentication       = "plain"
            mail.encryption           = :starttls
        end

6. To manually run the backup, use this command

        juan@ubuntu:~/seven$ psql -d seven_development -U juan -f ~/Desktop/PostgreSQL.sql -W

    The output should be like this

        [2016/09/05 15:49:24][info] Storing '/home/juan/backups/db_backup/2016.09.05.15.49.24/db_backup.tar'...
        ...
        [2016/09/05 15:49:24][warn] Backup for 'Description for db_backup (db_backup)' Completed Successfully (with Warnings) in 00:00:00

7. To test this, add some data in the DB, and then drop it, and re-create it

        juan@ubuntu:~/seven$ rails db:drop db:create

8. Then, restore it (first, unzip the previouslly created file)

        juan@ubuntu:~/seven$ psql -d seven_development -U juan -f ~/Desktop/PostgreSQL.sql -W

That's it! More on this in my next post.
