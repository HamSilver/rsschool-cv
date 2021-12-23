# Stanislav Kolpakov

## Contact information
- *Phone:* +7 921 006 9767
- *GitHub:* HamSilver
- *Email:* kolpakoff@gmail.com

***

## About me
In IT since the age of 12. )) Digital dinosaur. I remember FidoNet and modem sounds.<br />
I taught сomputer science at school: got stress resistance and conversation practice with native speaking Peace Corps volunteers, worked there.<br />
I worked in a bank as programmer: got knowledge of databases, security and backup importance.<br />
I wrote billing for an internet provider: dived into Perl, PHP, HTML and PostgreSQL.<br />
I worked as design engineer: had been drawing things in CAD.<br />
I worked as designer: just had been drawing.<br />
I worked as web designer/programmer: learned magic how to made working site from a pencil sketch. <br />
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
JS / jQuery form validating:
```javascript
function saveshop() {
  // debug 1:on / 0:off
	var debug=0;
	var err='';
	var sss=$.trim($("input[name=shopname]").val());
	var re = /^[A-ZА-Я0-9._\(\)\-\+\s]+$/i;  
	var ru = /^[A-ZА-Я.\-\s]+$/i;  
	var rd = /^[A-Z0-9\-\s]+$/i; 
	var em = /^[A-Z0-9._-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i;
	if ((sss.length<1)|(null == sss.match(re))) {
		err = 'Неправильно указано название торговой организации:\n-- допустимые знаки: А-Я A-Z 0-9 . _ + - ( )\n';
	}
	sss=$.trim($("input[name=postcode]").val());
	if (sss.length<4) {
		err += 'Почтовый индекс должен быть не менее 4 знаков.\n';
	} else
	if (null==sss.match(rd)) {
		err += 'Почтовый индекс может содержать только цифры, англйские буквы и знак тире.\n';
	}
	if ($("input[name=country_id]").val()=='null') {
		err += 'Не выбрана страна.\n';
	}
	if ($("input[name=city_id]").val()=='null') {
		err += 'Не выбран город.\n';
	}
	sss=$.trim($("input[name=ocity]").val());
	if (($("input[name=city_id]").val()=='-1')&(sss=='')) {
		err += 'Не указан населенный пункт.\n';
	} else
	if (($("input[name=city_id]").val()=='-1')&(null == sss.match(re))) {
		err += 'Название населенного пункта может содержать только буквы, цифры и знак тире.\n';
	}
	if ($.trim($("input[name=address]").val())=='') {
		err += 'Не указан адрес.\n';
	}
	if ($.trim($("input[name=phone]").val())=='') {
		err += 'Не указан номер телефона.\n';
	}
	sss=$.trim($("input[name=boss]").val());
	if ((sss.length<1)|(null == sss.match(ru))) {
		err += 'Неправильно указано Ф.И.О. руководителя:\n-- допустимые знаки: А-Я A-Z . -\n';
	}
	if (err=='') {
		$("input[name=key]").val(key);
		$("#ajaxload").show();
	  if (debug==0) {
		  $.post('/formaction.php', $("#addshopform").serialize(),
			function(data) {
				$("#ajaxload").fadeOut();
				if (data[0].result=='exec') {
					$("#ajaxpop").hide();
					$(".column").html(data[0].column);
					key=data[0].key;
					$("select[name=shop] option[text="+$("input[name=shopname]").val()+"]").attr("selected", true);
				} else 
     			show_err(data,'saveshop:ajax:send:1');
   			}, "json"
		  );
	  } else {
		  $.post('/formaction.php', $("#addshopform").serialize(),
			function(data){
				$("#ajaxload").fadeOut();
				alert(data);
   		}
		  );
	  }
	} else 
	  show_err(data,'saveshop:check:1');
}
```

Little bit of PHP:
```php
if ($numrow>0) {
	echo '[ { "result" : "error", "token" : "Указанный e-mail уже используется." } ]';
} else { 
// регистрируем
	$psw=ae_gen_password();
	$are=md5(''.microtime());
  $query = sprintf("INSERT INTO actioninfo (fname,nname,sname,postcode,country_id,region_id,city_id,ocity,address,phone,email,pass,reg) VALUES (%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)",
  quote_smart($fname),
  quote_smart($nname),
  quote_smart($sname),
  quote_smart($index),
  quote_smart($country_id),
  quote_smart($region_id),
  quote_smart($city_id),
  quote_smart($ocity),
  quote_smart($address),
  quote_smart($phone),
  quote_smart($email),
  quote_smart($psw),
  quote_smart($are)
  );
	$result=mysql_query($query) or die (mysql_error());
	require_once($_SERVER['DOCUMENT_ROOT'].'/class.phpmailer.php');
	$mail             = new PHPMailer();
	$mail->IsSendmail();
	$mail->CharSet    = "UTF8";
	$body             = '<body>Для активации учетной записи нажмите на ссылку: <a href="https://somesite/'.$are.'">https://somesite/'.$are.'</a><br />Ссылка действительна в течение 24 часов.</body>';
	$mail->AddReplyTo("no-reply@somesite","somesender");
	$mail->SetFrom('no-reply@somesite', 'somesender');
	$mail->AddAddress($email, $nname.' '.$fname);
	$mail->Subject    = "somesite activation";
	$mail->AltBody    = 'Use link for account activation: https://somesite/'.$are; 
	$mail->MsgHTML($body);
	if(!$mail->Send()) {
	  // "Mailer Error: " . $mail->ErrorInfo;
  	  echo '[ { "result" : "err", "token" : "Ошибка отправки письма: '.$mail->ErrorInfo.'" } ]';
	} else {
	  // "Message sent!";
  	  echo '[ { "result" : "regged", "token" : "На Ваш адрес электронной почты отправлена ссылка для активации." } ]';
	}
}
```

Perl example:
```perl
#!/usr/bin/perl
use XML::Simple;
use Data::Dumper;
my $simple = XML::Simple->new();
my $data   = $simple->XMLin('file.xml', KeyAttr => {'param'=>'id_param'}, ContentKey => '-content');
my $ofile = $ARGV[0] or die "Error: output file name not given\n";
open(my $rslt, '>:encoding(utf8)', $ofile) or die "Error: could not open '$ofile' $!\n";
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
I have experience in web and software development as I wrote above. 

***

## Education
**Dalnegorsk Evening Industrial College** (Now Dalnegorsk branch of Far Eastern Federal University)<br />
_Specialist's degree: Automated information processing and management systems_

***

## Languages
- **Russian** - native
- **English** - B1 (Intermediate)