# Converts MySQL dump (.sql) of db schema to a TSV file

Run this command in terminal
cat db_schema.sql | sed '/#.*/d; /\/\*.*\*\//d' | tr -d '\n' | tr ';' '\n' | sed 's/CREATE TABLE \`\([a-zA-Z_]*\)\` (\(.*\)).*/\1 \2/g' | while read tname cells; do echo "$cells" | tr ',' '\n' | while read l; do echo "$l"; done | cut -f 1,2 -d ' ' | sed '/^\`/!d; s/\`//g' | tr ' ' '\t' | while read i; do printf "%s\t%s\n" "$tname" "$i">>/tmp/b; done; done


You will find the TSV file in /tmp/b
