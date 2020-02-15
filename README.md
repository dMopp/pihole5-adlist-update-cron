# pihole5-adlist-update-cron
A pihole5 compatible cronjob to fetch Adlist(s) from URL and import them to the new gravity.db

# usage
- Place the file into /etc/cron.daily/
- `chmod +x /etc/cron.daily/update-adlist-list`
- Modify the Variables for you needs
- done

# cron spam?
If you dont like to have a daily cronmail, you can place the script somewhere else and:
## Errors should be send
- Create a file like this: `echo "bash /path/to/the/script > /dev/null" > /etc/cron.daily/update-adlist-list-silent`
- `chmod +x /etc/cron.daily/update-adlist-list-silent`
## No Errors should be send
- Create a file like this: `echo "bash /path/to/the/script > /dev/null 2>&1" > /etc/cron.daily/update-adlist-list-silent`
- `chmod +x /etc/cron.daily/update-adlist-list-silent`
