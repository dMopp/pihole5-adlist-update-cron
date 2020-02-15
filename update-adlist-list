#!/bin/bash
#####CHANGE STUFF HERE
PIHOLE_DIR="/etc/pihole"
ADLIST_URL="https://v.firebog.net/hosts/lists.php?type=nocross"
CLEAN_ADLISTS_BEFORE_UPDATE=true


#####DO NOT CHANGE
#####Variables
DATE=$(date '+%Y-%m-%d')
ADLIST="${PIHOLE_DIR}/adlists.list"
FLUSH_SQL="${PIHOLE_DIR}/FLUSH.sql"
IMPORT_SQL="${PIHOLE_DIR}/IMPORT.sql"
GRAVITY_DB="${PIHOLE_DIR}/gravity.db"


#####Fetch Files
echo "Downloading Adlist(s)"
wget -O ${ADLIST} ${ADLIST_URL}

#####GENERATE SQL
echo "Generating SQL files..."
cat <<EOF > ${FLUSH_SQL}
DELETE FROM adlist;
EOF

cat <<EOF > ${IMPORT_SQL}
CREATE TEMP TABLE i(txt);
.separator ~
.import ${ADLIST} i
INSERT OR IGNORE INTO adlist (address) SELECT txt FROM i;
DROP TABLE i;
EOF

#####CLEANUP DB (if selected)
if ${CLEAN_ADLISTS_BEFORE_UPDATE}; then
	echo "Cleanup DB..."
	sqlite3 ${GRAVITY_DB} < ${FLUSH_SQL}
fi

#####IMPORT FILE to DB
echo "Import Adlist(s)..."
sqlite3 ${GRAVITY_DB} < ${IMPORT_SQL}
pihole -g

###CLEANUP
echo "Cleaning up..."
rm ${ADLIST}
rm ${FLUSH_SQL}
rm ${IMPORT_SQL}
