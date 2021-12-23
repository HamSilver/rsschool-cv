# Stanislav Kolpakov

## Contact information
- *Phone:* +7 921 006 9767
- *GitHub:* HamSilver
- *Email:* kolpakoff@gmail.com
***
## About me
In IT since the age of 12. )) Digital dinosaur. I remember FidoNet and modem sounds. 
I taught сomputer science at school: got stress resistance and conversation practice with native speaking Peace Corps volunteers, worked there.
I worked in a bank as programmer: got knowledge of databases, security and backup importance.
I wrote billing for an internet provider: dived into Perl, PHP, HTML and PostgreSQL.
I worked as design engineer: had been drawing things in CAD.
I worked as designer: just had been drawing.
I worked as web designer/programmer: learned magic how to made working site from a pencil sketch. 
Keep learning.
***
## Skills
* PHP / Perl / Python / C++ / Delphi / FoxPro / VBA / JS
* MSSQL / MySQL / PgSQL / Interbase 
* HTML / CSS
* jQuery / React
* GIT / GitHub
* Windows / Linux 
* Figma
* Photoshop / CorelDraw / InDesign
* 3DS Max / Creo / NX
***
## Code sample
Random JS solution for Codewars:
```javascript
function rgb(r, g, b){
  return [r,g,b].map(x => x>255 ? 255 : x).map(x => x>0 ? ("0"+((x).toString(16))).slice(-2).toUpperCase() : '00').join('');
}
```
Little bit of some PHP:
```php
      $database=b_connect();
      // ajax
      require_once "lib/JsHttpRequest/JsHttpRequest.php";
      $JsHttpRequest =& new JsHttpRequest("koi8-r");
      $uid=(int)$_REQUEST['uid'];
      $tid=(int)$_REQUEST['tid'];
      $state=(real)$_REQUEST['state'];
      // get user state
      $query="SELECT check_user_connect($uid,$tid,get_balans($uid));";
      $result = pg_exec ($database, $query);
      if (!$result) {
          // catch error
	        echo "Query:$query<br>An error occured (users:onofftarif:check_user_connect)\n";
   	      exit;
      } 
```
```perl
#!/usr/bin/perl
use XML::Simple;
use Data::Dumper;
my $simple = XML::Simple->new();
my $data   = $simple->XMLin('file.xml', KeyAttr => {'param'=>'id_param'}, ContentKey => '-content');
my $ofile = $ARGV[0] or die "Error: output file name not given\n";
open(my $rslt, '>:encoding(utf8)', $ofile) or die "Could not open '$ofile' $!\n";
# for first thousand
for (my $i=0; $i <= 999; $i++) {
	if ($data->{group}{record}[$i]) {
		$nm=$data->{group}{record}[$i]{param}{96};
		if ((!($nm=~ m/(a|c)3$/i))&&($nm=~ m/([a-z0-9]{4}\w3)/i)) {
			$art=$1;
			$id=$data->{group}{record}[$i]{group}{record}{param};
			$px="".$id->{129}.$id->{102}.$id->{136}."";
			$id=$data->{group}{record}[$i]{group}{record}{group}{record}{param};
			$tx="".$id->{130}.$id->{131}.$id->{132}.$id->{133}."";
				print $rslt "$art\n";
		}
	}
}
close $rslt;
```
***
## Expirience


***
## Education
Mainly online/books self-education
***
## English level
B1 (Intermediate)