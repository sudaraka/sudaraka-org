{
  "title": "ADSL (SLT) භාවිතාකරන්නන්ට උපදෙසක්",
  "description": "Tip for (SLT) ADSL Users - how to make the ADSL router maintain a stable connection",
  "keywords": "ADSL,router,configuration,stable,connection,snr,modulation",
  "date": "2012-11-17"
}

පසුගිය දිනවල මගේ ADSL සම්බන්ධතාවයේ පැවති දෝශයක් නිරාකරණය කරගැනීමේදී දැනගත් කරුණු
කිහිපයක් සියලුදෙනාගේ දැනගැනීම සඳහා ඉදිරිපත් කරන්න හිතුනා.<!--more-->

## දෝශය
මගේ සම්බන්ධතාවයේ දෝශය උනේ එකදිගට සම්බන්ධතාවය නොපැවතීමයි. එනම් විනාඩි 5න් 5ට
සම්බන්ධතාව විසන්ධිවීමයි, මේ තත්වය පසුගිය ඔක්තෝබර් මාසයේ මුල සිට තදින්ම පැවතුනා,
සම්බන්ධතාව භාවිතා කරන්න බැරිම මට්ටමකට පත්වුන නිසා දෝශ වාර්තා කිරීමක් කලා.

## විසඳුම
මේ පිළිබඳ පරීක්ෂාකර බැලීමට නිවසට පැමිනි තාක්ෂණ ශිල්පියා පැවසූ ආකාරයට, රවුටරයේ
(හෝ මොඩමයේ) ADSL Mode (modulation) යන්න G.DMT (හෙවත් G.992.1) ලෙස යෙදීමෙන්
සම්බන්ධතාවයේ අස්ථාවරබව
මගහරවාගත හැකියි.

![TP-LINK ADSL2+ Router - ADSL Mode](/images/chronicles/tip-for-slt-adsl-users-01.png)
![PROLiNK ADSL2+ Router - ADSL Modulation](/images/chronicles/tip-for-slt-adsl-users-04.png)

තවද, ස්ථාවර සම්බන්ධතාවකට ADSL තොරතුරු වල දැක්වෙන SNR margin අගය 11ට වැඩි අගයක්
ගතයුතු වෙනවා.

![TP-LINK ADSL2+ Router - SNR](/images/chronicles/tip-for-slt-adsl-users-02.png)
![PROLiNK ADSL2+ Router - SNR](/images/chronicles/tip-for-slt-adsl-users-03.png)

ඉහත ආකාරයෙන් අදාල සැකසුම් කිරීමෙන් පසු මගේ ADSL සම්බන්ධතාව ස්ථාවරව ඉතා හොඳින්
පවතිනවා.

## පසු විපරම
කෙනෙක් කියූ පමනින් යමක් පිළිගැනීමෙ පුරුද්දක් නැති නිසා මේගැන තව තොරතුරු අන්තර්ජාලය
ඔස්සේ සොයා බැලුවා. එහිදී හමුවූ කරුණු ස්වල්පයක් පහත දැක්වෙනවා.

__සැ.යු.__
_අන්තර්ජාලයේ ඇති තොරතුරු "සියල්ල සත්‍ය" නිසාත්, මෙම සමහර පැහැදිලි කිරීම් මගේ උපකල්පන
නිසාත් මේවා පිළිබඳ තවදුරටත් සොයා බලන්න._

### SNR margin
[Signal to Noise Ratio](https://en.wikipedia.org/wiki/Signal-to-noise_ratio) (SNR) යනු ඕනෑම සංඥා
හුවමාරුවකදී අදාල මාධ්‍යයේ ඇති ඝෝශාවේ (Noise) සහ නිවැරදි සංඥාවේ බලය අතර අනුපාතය වන
අතර SNR [margin](https://en.wikipedia.org/wiki/Noise_margin) යනු ඝෝශාවට වඩා සංඥාවේ බලය කෙතරම් ඉදිරියෙන්
ඇත්ද යනවග දක්වන අගයකි.

එනම් එම අගය වැඩි වනවිට හොඳ සංඥාවක් ලැබෙන බව උපකල්පනය කිරීමට පුලුවන්. ඒ අනුව ඉහත
සඳහන් කල තාක්ෂණ ශිල්පියා කියනලද කරුණ සත්‍යයක්.

තවදුරටත්, [විකිපීඩියා ADSL ලිපියේ](https://en.wikipedia.org/wiki/Asymmetric_digital_subscriber_line#Operation)
මෙලෙස සඳහන් වෙනවා:

> A high SNR margin will mean a reduced maximum throughput, but greater reliability and stability of the connection. A low SNR margin will mean high speeds, provided the noise level does not increase too much; otherwise, the connection will have to be dropped and renegotiated (resynced)

&nbsp;

### ADSL Mode/modulation
Modulation යනු යම් සංඥාවක් විද්‍යුත් හෝ ද්‍රුශ්‍ය තරංගයක ගැබ් කිරීමේ ක්‍රමවේදයකි. ADSL සඳහා
මෙවැනි [modulation කිහිපයක්](https://en.wikipedia.org/wiki/Asymmetric_digital_subscriber_line#ADSL_standards)
භාවිතවේ.

මෙම එක් එක් modulation නිවැරදිව ක්‍රියාකිරීම සඳහා අදාල සංඥාවේ ගුණාත්මක බව ඍජුවම බලපාන
අතර, [G.DMT](https://en.wikipedia.org/wiki/G.DMT#DMT_history_and_line_rates) වැනි පැරණි modulation අඩු
ධාරිතාවක් (bandwidth) වැඩි දුරක් ගුණාත්මක භාවය රඳවාගනිමින් ගෙනයාහැකි ආකාරයට සකස් කර
ඇත. ADSL2+ වැනි නව modulation වැඩි ධාරිතාවකින් යුත් නමුත් සංඥාවේ ගුණාත්මක බව රඳවා ගත
හැකි දුර ප්‍රමානය අඩුවේ.

### දුර්වල රැහැන් සම්බන්ධතා
අප බොහෝ දෙනකුගේ නිවෙස්වලට සම්බන්ධ වන දුරකතන රැහැන් බොහෝවිට වසර 20කට හෝ ඊට
වැඩි කාලයකට පෙර සවිකරල ලද ඒවා වන අතර, ඒවා කිසිදු ප්‍රමිතියකින් තොරව විදුලි රැහැන් සමග
එකට පටලා සවිකර ඇති ආකාරය ඕනෑම ප්‍රදේශයක දැකගැනීමට ඇත. එමෙන්ම බෙදුම් පෙට්ටි සහ විවිධ
පරිපථ අඩංගු කොටස් විවෘතව ජලය කාන්දුවිය හැකි අයුරෙන් පවතී.

මෙම හේතු සහ වෙනත් ස්වාභාවික හේතු නිසා අපගේ නිවසට ලැබෙන දුරකතන සංඥාවේ දුර්වලතා පවතී.
දුරකතන ඇමතුමක් ලබාගැනීමේදී මෙය බලපෑමක් නොවුනද ADSL සම්බන්ධතාවයේ දී මෙම සංඥාවේ
පවතින ගුණාත්මක භාවයේ හදිසි අඩු වැඩිවීම් ස්ථාවර සම්බන්ධතාවක් පවත්වාගැනීමට බාධා ඇතිකරයි.

### නවීන (ADSL2+) රවුටර
අද වෙලඳපොලේ ඇති බොහෝ රවුටර ADSL2+ වන අතර ඒවා G.DMT ඇතුලු පැරණි modulation
වලටද සහය දක්වයි.

ඉහත රූප සටහන් වල පෙන්වා ඇති ආකාරයට අදාල modulationඑක අපට තෝරාගත හැකි අතර,
බොහෝ විට පෙරනිමියෙන් එය Auto ලෙස සකස් වී ඇත. එනම් රවුටරය එයට ලැබෙන සංඥාවේ
ගුණාත්මක බව අනුව අදාල modulation එක තෝරා ගනී.

ඒ අනුව සම්බන්ධතාව අතරමැදදී සංඥාව දුර්වලවූ විට රවුටරය විසින් modulation වෙනස් කිරීමට උත්සාහ
ගන්න බැවින් සම්බන්ධතාව විසන්ධිවේ.
