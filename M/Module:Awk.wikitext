local p = {}
 
function p.help( frame )
    return "Usage: awk [POSIX or GNU style options] -f progfile [--] file ...<br />Usage: awk [POSIX or GNU style options] [--] 'program' file ...<br />POSIX options: GNU long options:<br /> -f progfile --file=progfile<br /> -F fs --field-separator=fs<br /> -v var=val --assign=var=val<br /> -m[fr] val<br /> -O --optimize<br /> -W compat --compat<br /> -W copyleft --copyleft<br /> -W copyright --copyright<br /> -W dump-variables[=file] --dump-variables[=file]<br /> -W exec=file --exec=file<br /> -W gen-po --gen-po<br /> -W help --help<br /> -W lint[=fatal] --lint[=fatal]<br /> -W lint-old --lint-old<br /> -W non-decimal-data --non-decimal-data<br /> -W profile[=file] --profile[=file]<br /> -W posix --posix<br /> -W re-interval --re-interval<br /> -W source=program-text --source=program-text<br /> -W traditional --traditional<br /> -W usage --usage<br /> -W use-lc-numeric --use-lc-numeric<br /> -W version --version<br /><br />To report bugs, see node `Bugs' in `gawk.info', which is<br />section `Reporting Problems and Bugs' in the printed version.<br /><br />gawk is a pattern scanning and processing language.<br />By default it reads standard input and writes standard output.<br /><br />Examples:<br /> gawk '{ sum += $1 }; END { print sum }' file<br /> gawk -F: '{ print $1 }' /etc/passwd"

end
 
return p