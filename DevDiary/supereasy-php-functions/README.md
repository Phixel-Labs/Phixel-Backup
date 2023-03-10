# Save time with some PHP functions 🚀🤖 (Part 1)
### As PHP developers, we all know the struggle of trying to remember every native PHP function.

It can be like trying to recall your high school locker combination after years of not using it. Was it strtolower() or str_lower()? And what about the difference between htmlentities() and html_entity_decode()?

It’s a problem we’ve encountered time and time again, so we’ve come up with a solution. We’ve developed a suite of functions to make our lives as PHP developers a little easier. Our functions cover various areas of PHP development, including string manipulation, working with HTML and URLs, and array manipulation.

#### Case fix

```php
<?php
/*
Title: Convert string to uppercase
Description: This function takes a string as input and returns the string in uppercase format after removing extra spaces.
*/
function upperCase( $str ){
$str = preg_replace( '/\s+/', ' ', $str );
return strtoupper( $str );
}
?>

```

```php
<?php
/*
Title: HTML Decode
Description: Converts HTML encoded characters to their original character representation.
*/
function html_decode( $str ){
return html_entity_decode( $str );
}
function htmlDecode( $str ){
return html_decode( $str );
}
function decodeCase( $str ){
return html_decode( $str );
}
?>

```

```php
<?php
/*
Title: Title Case
Description: Converts a given string to title case.
Note: Id changes back lower case articles an support latin characters.
*/
function titleCaseFix($str) {
$str = str_replace('Ñ', 'ñ', $str);
$str = str_replace('Á', 'á', $str);
$str = str_replace('É', 'é', $str);
$str = str_replace('Í', 'í', $str);
$str = str_replace('Ó', 'ó', $str);
$str = str_replace('Ú', 'ú', $str);
$str = str_replace('Ü', 'ü', $str);
$str = str_replace('Â¿', '¿', $str);
$str = str_replace('# ', '#', $str);
$str = str_replace(' #', '#', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace('-', ' - ', $str);
$str = str_replace(', ', ' , ', $str);
$str = str_replace('.', '. ', $str);
$str = str_replace(':', ': ', $str);
$str = str_replace('__', ' - ', $str);
$str = str_replace(' :', ': ', $str);
$str = str_replace('>', '> ', $str);
$str = str_replace('<', ' <', $str);
$str = str_replace('(', '( ', $str);
$str = str_replace(')', ' )', $str);
$str = str_replace('¿', '¿ ', $str);
$str = str_replace('?', ' ?', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = utf8_decode($str);
$str = strtolower($str);

$str = trim($str).' ';
$arr = strtolower($str);
$str = ucwords($str);

$minus = array(
'la', 'el', 'en', 'to', 'es', 'un', 'lo', 'su', 'sus', 'a', 
'sobre', 'de', 'los', 'las', 'suyo', 'su', 'este', 'y', 
'ese', 'mi', 'tu', 'soy', 
'del', 'de', 'o', 'u', 'e', 'con', 

'a', 'an', 'the', 'and', 'but', 'or', 'for', 'nor', 
'as', 'at', 'by', 'for', 'from', 'in', 'into', 'near', 
'of', 'on', 'onto', 'to', 'with'
);
foreach($minus as $key => $value){
$value = strtolower($value);
$value = ucwords($value);
$value = ' '.($value).' ';
$str = str_replace(($value), strtolower($value), $str);
}
$mayus = array(
'B2B', 'B2C', 'MEV', 'TUT', 'EIA', 'ID', 'CDE', 'DHT', 'SAC', 
'DTH', 'FV', 'FVD', 'TV', 'HD', 'KPI', 'CNC', '1Q', '2Q', 'EYG', 
'CNV', 'CU', 'CNT', 'HFC', 'PRI', 'ATN', 'PON', 'OTRD', 'RDSI', 
'SIP', 'PQR', 'CPV', 'ATA', 'STB', 'RTL', 'FVD', 'CPE', 'PRO'.
'3G', '4G', 'ATP', 'TTT', 'PO', 'AI', 'JavaScript', 'JS'
);
foreach($mayus as $key => $value){
$value = strtolower($value);
$value = ucwords($value);
$value = ($value).' ';
$str = str_replace(($value), strtoupper($value), $str);
}
$str = str_replace('#', ' # ', $str);
$str = str_replace('( ', '(', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' )', ') ', $str);
$str = str_replace(':', ': ', $str);
$str = str_replace(' , ', ', ', $str);
$str = str_replace(' , ', ', ', $str);
$str = str_replace('¿ ', ' ¿', $str);
$str = str_replace(' ?', '? ', $str);
$str = str_replace(' :', ':', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = str_replace(' ', ' ', $str);
$str = trim($str);
$str = utf8_encode($str);
return $str;
}

function titleCase($str) {
return titleCaseFix($str);
}
?>

```

```php
<?php
/*
Title: Clean a string for a code-friendly format
Descrition: This function takes in a string and sanitizes it for use in code by converting it to lowercase, removing special characters, and replacing spaces with a specified separator. Optionally, it can also remove common English words such as articles and prepositions.
*/
function cleanCase($str , $char = '_', $union = true){

//decode any html entities
$str = html_entity_decode($str);

//convert the string to lower case
$str = lowerCase(' '.$str.' ');

//convert utf-8 to ascii
$str = @iconv('UTF-8', 'ASCII//TRANSLIT', $str);

// removing special characters
$str = str_replace("'", '', $str);
$str = str_replace("~", '', $str);

// Remove any non-alphanumeric characters
$str = preg_replace("/[^A-Za-z0-9 ]/", ' ', $str);

// Replace multiple spaces with a single space
$str = str_replace(trim(" \ "), ' ', $str);
$str = str_replace("/", ' ', $str);
$str = preg_replace('/\s+/', ' ', $str);

if($union){
$minus =array(
'la', 'el', 'en', 'to', 'es', 'un', 'lo', 'su', 'sus', 'a', 
'sobre', 'de', 'los', 'las', 'suyo', 'su', 'este', 'y', 
'aquel', 'ese', 'mi', 'tu', 'nuestro', 'vuestro', 'soy', 
'del', 'de', 'o', 'u', 'e', 'con', 

'a', 'an', 'the', 'and', 'but', 'or', 'for', 'nor', 
'as', 'at', 'by', 'for', 'from', 'in', 'into', 'near', 
'of', 'on', 'onto', 'to', 'with'
);

foreach($minus as $key => $value){
$str = str_replace(' '.$value.' ', ' ', $str);
}
}
$str = preg_replace('/\s+/', ' ', $str);
$str = trim($str);
$str=str_replace(' ', $char, $str);
return ($str);
}

function caseClear($str, $char = '-'){
return cleanCase($str, $char);
}
function caseClean($str, $char = '-'){
return cleanCase($str, $char);
}

function clearCase($str, $char = '-'){
return cleanCase($str, $char);
}
function str_clean($str, $char = '-'){
return cleanCase($str, $char);
}

function str_clear($str, $char = '-'){
return cleanCase($str, $char);
}
?>

```

#### Encode decode fix

```php
<?php
/*
Title: HTML Encoding
Description: Converts special characters to HTML entities, making it safe to display on a web page.
*/
function html_encode( $str ){
return htmlentities( $str );
}
function htmlEncode( $str ){
return html_encode( $str );
}
function encodeCase( $str ){
return html_encode( $str );
}
?>

```

```php
<?php
/*
Title: Convert string to uppercase
Description: This function takes a string as input and returns the string in uppercase format after removing extra spaces.
*/
function upperCase( $str ){
$str = preg_replace( '/\s+/', ' ', $str );
return strtoupper( $str );
}
?>

```

```php
<?php
/*
Title: URL Decode
Description: This function takes a string encoded with URL encoding and decodes it back to its original form.
*/
function url_decode ( $str ){
return urldecode ( $str );
}
?>

```

```php
<?php
/*
Title: URL Encode Function
Description: This function takes a string as input and returns the URL encoded version of the string.
*/
function url_encode ( $str ){
return urlencode ( $str );
}
?>

```

#### Numbers fix

```php
<?php
/*
Title: Convert Integer to Percentage
Description: This function takes an integer and converts it to a percentage based on a total value. The function has options to return the result as a plain number, with only the percentage, or with both the integer and total values.
*/
function convert_percent( $int = 0, $total = 100, $off = 'false' ){
$t = ( round( ( round( $int )*100 )/round( $total ) ).'' )*1;
$int_n = number_format( $int*1 );
$t_n = number_format( $t*1 );
$total_n = number_format( $total*1 );
if( $off == 'false' ){
return( $int_n.' ( '.$t_n.'% )' );
}else if( $off == 'number' ){
return( $t );
} else if( $off == 'true' ){
return( $int_n.'/'.$total_n.' ( '.$t.'% )' );
}
}
function per( $int = 0, $total = 100, $off = 'false' ){
return convert_percent( $int, $total, $off );
}

function percent( $int = 0, $total = 100, $off = 'false' ){
return convert_percent( $int, $total, $off );
}

function per_e( $int = 0, $total = 100, $off = 'false' ){
e( per( $int, $total, $off ) );
}

```

```php
<?php
/*
Title: Format number function
Description: Converts a number to a formatted string
*/
function numberFormat( $num ){
$str = $num*1;
$str = number_format($str);
return ( $str );
}

```

```php
<?php
/*
Title: Lead Zero
Description: Adds a leading zero to a number if its length is less than 2
*/

function leadZero($num, $length = 2) {
$num = round($num);
return (strlen($num) < $length) ? "0{$num}" : $num;

}

function lead_zero($num, $length = 2) {
return leadZero($num, $length);
}

```

#### Number conversion fix

```php
<?php
/*
Title: File Size Conversion
Description: This function takes the file size in bytes and converts it into the appropriate size unit (TB, GB, MB, KB or Bytes)
*/

function fileSize($bytes, $power = 1024){
$bytes = floatval($bytes);
$arBytes = array(
0 => array(
"UNIT" => "TB", 
"VALUE" => pow($power, 4)
), 
1 => array(
"UNIT" => "GB", 
"VALUE" => pow($power, 3)
), 
2 => array(
"UNIT" => "MB", 
"VALUE" => pow($power, 2)
), 
3 => array(
"UNIT" => "KB", 
"VALUE" => $power
), 
4 => array(
"UNIT" => "Bytes", 
"VALUE" => 1
), 
);

foreach($arBytes as $arItem){
if($bytes >= $arItem["VALUE"]){
$result = $bytes / $arItem["VALUE"];
$result = str_replace(".", "." , strval(round($result, 2)))." ".$arItem["UNIT"];
break;
}
}
return $result;
}

function file_size($bytes, $power = 1024){
return fileSize($bytes, $power);
}

```

```php
<?php
/*
Title: Weight Conversion
Description: This function takes the object weight in grams and converts it into the appropriate weight unit (Tons, Kilograms, Grams)
*/

function weight($grams, $power = 1000){
$grams = floatval($grams);
$arGrams = array(
0 => array(
"UNIT" => "Tons", 
"VALUE" => pow($power, 3)
), 
1 => array(
"UNIT" => "Kilograms", 
"VALUE" => $power
), 
2 => array(
"UNIT" => "Grams", 
"VALUE" => 1
), 
);

foreach($arGrams as $arItem){
if($grams >= $arItem["VALUE"]){
$result = $grams / $arItem["VALUE"];
$result = str_replace(".", ".", strval(round($result, 2)))." ".$arItem["UNIT"];
break;
}
}
return $result;
}

```

```php
<?php
/*
Title: Liquid volume Conversion
Description: This function takes the volume of liquid in milliliters and converts it into the appropriate size unit (L, dL, cL, mL or μL)
*/

function volume($ml, $power = 10){
$ml = floatval($ml);
$arMl = array(
0 => array(
"UNIT" => "L", 
"VALUE" => pow($power, 3)
), 
1 => array(
"UNIT" => "dL", 
"VALUE" => pow($power, 2)
), 
2 => array(
"UNIT" => "cL", 
"VALUE" => $power
), 
3 => array(
"UNIT" => "mL", 
"VALUE" => 1
), 
4 => array(
"UNIT" => "μL", 
"VALUE" => pow(10, -3)
), 
);

foreach($arMl as $arItem){
if($ml >= $arItem["VALUE"]){
$result = $ml / $arItem["VALUE"];
$result = str_replace(".", "." , strval(round($result, 2)))." ".$arItem["UNIT"];
break;
}
}
return $result;
}

?>

```

```php
<?php
/*
Title: Month names in Spanish or english
Description: Return the name of the month based on the number.
*/
function month( $date = 1 , $lang = 'es'){
$dates['es'] = array(
'Enero', 
'Febrero', 
'Marzo', 
'Abril', 
'Mayo', 
'Junio', 
'Julio', 
'Agosto', 
'Septiembre', 
'Octubre', 
'Noviembre', 
'Diciembre'
);
$dates['en'] = array(
'January', 
'February', 
'March', 
'April', 
'May', 
'June', 
'July', 
'August', 
'September', 
'October', 
'November', 
'December'
);
return $dates[ $lang ][ ( $date-1 ) ];
}
?>

```

```php
<?php
/*
Title: File Size Conversion
Description: This function takes the file size in bytes and converts it into the appropriate size unit (TB, GB, MB, KB or Bytes)
*/

function fileSize($bytes, $power = 1024){
$bytes = floatval($bytes);
$arBytes = array(
0 => array(
"UNIT" => "TB", 
"VALUE" => pow($power, 4)
), 
1 => array(
"UNIT" => "GB", 
"VALUE" => pow($power, 3)
), 
2 => array(
"UNIT" => "MB", 
"VALUE" => pow($power, 2)
), 
3 => array(
"UNIT" => "KB", 
"VALUE" => $power
), 
4 => array(
"UNIT" => "Bytes", 
"VALUE" => 1
), 
);

foreach($arBytes as $arItem){
if($bytes >= $arItem["VALUE"]){
$result = $bytes / $arItem["VALUE"];
$result = str_replace(".", "." , strval(round($result, 2)))." ".$arItem["UNIT"];
break;
}
}
return $result;
}

function file_size($bytes, $power = 1024){
return fileSize($bytes, $power);
}

```

```php
<?php
/*
Title: Time Conversion
Description: This function takes the time in seconds and converts it into the appropriate unit (years, decades, centuries, milliseconds, days, months or seconds)
*/

function time($time, $power = 1) {
$time = floatval($time);
$arTime = array(
0 => array(
"UNIT" => "Milliseconds", 
"VALUE" => pow($power, -3)
), 
1 => array(
"UNIT" => "Seconds", 
"VALUE" => $power
), 
2 => array(
"UNIT" => "Minutes", 
"VALUE" => 60 * $power
), 
3 => array(
"UNIT" => "Hours", 
"VALUE" => 60 * 60 * $power
), 
4 => array(
"UNIT" => "Days", 
"VALUE" => 24 * 60 * 60 * $power
), 
5 => array(
"UNIT" => "Months", 
"VALUE" => 30 * 24 * 60 * 60 * $power
), 
6 => array(
"UNIT" => "Years", 
"VALUE" => 365 * 24 * 60 * 60 * $power
), 
7 => array(
"UNIT" => "Decades", 
"VALUE" => 10 * 365 * 24 * 60 * 60 * $power
), 
8 => array(
"UNIT" => "Centuries", 
"VALUE" => 100 * 365 * 24 * 60 * 60 * $power
), 
9 => array(
"UNIT" => "Millenniums", 
"VALUE" => 1000 * 365 * 24 * 60 * 60 * $power
)
);

foreach($arTime as $arItem) {
if ($time >= $arItem["VALUE"]) {
$result = $time / $arItem["VALUE"];
$result = str_replace(".", ".", strval(round($result, 2))) . " " . $arItem["UNIT"];
break;
}
}
return $result;
}

```

```php
<?php
/*
Title: Temperature Conversion in Celsius
Description: This function takes temperature in Kelvin and converts it into Celsius.
*/

function temperatureConversion($temp, $power = 1){
$temp = floatval($temp);
$arTemperature = array(
0 => array(
"UNIT" => "m°C", 
"VALUE" => pow($power, -3)
), 
1 => array(
"UNIT" => "µ°C", 
"VALUE" => pow($power, -6)
), 
2 => array(
"UNIT" => "n°C", 
"VALUE" => pow($power, -9)
), 
3 => array(
"UNIT" => "p°C", 
"VALUE" => pow($power, -12)
), 
4 => array(
"UNIT" => "°C", 
"VALUE" => 1
), 
);

foreach ($arTemperature as $arItem) {
if ($temp >= $arItem["VALUE"]) {
$result = $temp / $arItem["VALUE"];
$result = str_replace(".", ".", strval(round($result, 2))) . " " . $arItem["UNIT"];
break;
}
}
return $result;
}

```

#### Sring fix

```php
<?php
/*
Title: Clean the echo string
Description: Takes in a string as an input, and performs several operations to clean the string, specially for latin character.
*/
function e( $str = '' , $echo = true) {
// Set status of tilde
$hasTilde = false;

// Replace newline with space
$str = str_replace( '
', ' ', $str );

//replace non-breaking space with space
$str = str_replace( '&nbsp', ' ', $str );

// Checking if any latin characters are present
$hasTilde = preg_match('/[áéíóúñüÁÉÍÓÚÑÜ]/', $str);

// Replacing multiple spaces with single space
$str = preg_replace( '/\s+/', ' ', $str );

// Replace \n with newline
$str = str_replace( '\n', '
', $str );

// If there is not a tilde, UTF8 encode
if (!$hasTilde) {
$result = utf8_encode($str);
} else {
$result = $str;
}
if ($echo){
echo $result;
return = false;
}else {
return = $result ;
}

}
?>

```

```php
<?php
/*

Title: Convert an array to an HTML Unsorted List list quickly.
Description: Works with multi arrangements
Sample:
<ul>
<li><b>$value</b> is the name of the array.</li>
<li><b>$ul</b> Determines whether to create the opening and closing UL in html.</li>
</ul>
*/
function array2ul( $array = '', $id = 'list_', $keys = false, $vars = false, $title = false, $href = false ) {
$random = rand( 1000, 9999 );
if( $id == 'list' ){
$id = $id.$random;
}
ob_start();
?>
<ul
id="<? e( $id ); ?>"
class="padding-top-1 padding-bottom-1 "
<?
if( is_array( $vars ) ){
foreach ( $vars as $key => $value ) {
e( ' '.$key.'="'.$value.'"' );
}
}
?>
>
<?
if( is_array( $array ) ){
$i = 0;
foreach ( $array as $key => $value ) {
$id_ = cleanCase( $id.'_item_'.$key );
?>
<li
id="<? e( $id_ ); ?>"
data-item="<? e( $key ); ?>"s
data-list="<? e( $i ); ?>"
class="list padding-left-1"
>
<?
if( is_array( $value ) ){
array_ul( $value, $id_, $keys, false, $title, $href );
}else{
$v = trim( $value );
if( $keys ){
$v = '{_n}<b class="{color/primary}">'.$key.':</b>{_n}{_}'.$v;
}
if( $title ){
$v = '[ '.$title.$v.' ]';
}
if( $href ){
?>
<a href="<? e( $href ); ?><? e( cleanCase( $key ) ); ?>">
<? e( $v ); ?>
</a>
<?
}else{
e( $v );
}
}
?>
</li>
<?
$i++;
}

}else{
e( '{error-no-array}' );
}
?>
</ul>
<?
$html = ob_get_clean();
return $html;
}
function array_ul( $array = '', $id = 'list_', $keys = false, $vars = false, $title = false, $href = false ) {
return array2ul( $array, $id, $keys, $vars, $title, $href);
}

function array_to_ul( $array = '', $id = 'list_', $keys = false, $vars = false, $title = false, $href = false ) {
return array2ul( $array, $id, $keys, $vars, $title, $href);
}

?>

```

```php
<?php
/*
Title: Format an PHP array to be HTML friendly
Description: Return the array as a list.
*/
function print_html( $array, $title = '', $session = false) {

if ( $_SERVER[ "SERVER_NAME" ] == 'localhost' ) {
$bt = debug_backtrace();
$rand = dechex(rand(1000000, 9999999));
$nam = 'print_'.$rand;

ob_start();
if(!$title){
$title = '{text/print}: '.$rand;
}else{
$title = '<span class="yellow">{text/print}</span>: '.$title;
}
?>
<a
href="#print_<? e($rand); ?>"
onClick="
$('#print_<? e($rand); ?> .content').toggleClass('hidden');
$('#print_<? e($rand); ?>').toggleClass('hide');
"
class="{css/dark-bt}"
>
<? i('code console'); ?> <? e($title ); ?>
</a>
<div class="content hidden row ">
<div class="cont {css/padding} bg-dark round">

<h2 class="line padding-left-1 margin-bottom-1 padding-bottom-1 w-full row primary br-bottom-1">
<? e($title); ?>
</h2>

<div class="line padding-left-1 margin-bottom-1 padding-bottom-1 w-full row br-bottom-1">
<?php
e( '<h6 class="{css-col/full}"><b>{text/print-file} </b><i class="primary">'.$bt[1]['file'].'</i></h6>');
e( '<h6 class="{css-col/full}"><b>{text/print-line}</b> <i class="secondary">'.$bt[1]['line'].'</i></h6>');

if(is_array($array)){
e( '<h6 class="{css-col/full}"><b>{text/print-entries}</b><i class="orange">'.count($array).'</i></h6>');
}
?>
</div>

<div class="lists padding-bottom-1 w-full row">
<?php
if(is_array($array)){
foreach ($array as $key => $value) {
e('<div class="{css/padding}"><div class="list {css/padding} br-bottom-1 br-primary bg-dark round">');
e('<h5 class="secondary">'.$key.'</h5>');
if(is_array($value)){
array_ul($value, 'print_list_', true);
}else{
e('<p class="sm">'.$value.'</p>');
}
e('</div></div>');

}

}else{
e('<div class="list padding-left-1 {css-col/full}">');
e($array);
e('</div>');
}
?>
</div>

</div>
</div>
<?php

$print_h = ob_get_clean();
if($session){
return $_SESSION['print_html'][$title]= $print_h;
}else{
return ('<div class="print hide shadow row" id="print_'.$rand.'">'.$print_h.'</div>');
}
}
}

function print_h( $array, $title = '', $session = false ) {
return print_html( $array, $title, $session);
}

?>

```

```php
<?php
/*
Title: Time Conversion
Description: This function takes the time in seconds and converts it into the appropriate unit (years, decades, centuries, milliseconds, days, months or seconds)
*/

function time($time, $power = 1) {
$time = floatval($time);
$arTime = array(
0 => array(
"UNIT" => "Milliseconds", 
"VALUE" => pow($power, -3)
), 
1 => array(
"UNIT" => "Seconds", 
"VALUE" => $power
), 
2 => array(
"UNIT" => "Minutes", 
"VALUE" => 60 * $power
), 
3 => array(
"UNIT" => "Hours", 
"VALUE" => 60 * 60 * $power
), 
4 => array(
"UNIT" => "Days", 
"VALUE" => 24 * 60 * 60 * $power
), 
5 => array(
"UNIT" => "Months", 
"VALUE" => 30 * 24 * 60 * 60 * $power
), 
6 => array(
"UNIT" => "Years", 
"VALUE" => 365 * 24 * 60 * 60 * $power
), 
7 => array(
"UNIT" => "Decades", 
"VALUE" => 10 * 365 * 24 * 60 * 60 * $power
), 
8 => array(
"UNIT" => "Centuries", 
"VALUE" => 100 * 365 * 24 * 60 * 60 * $power
), 
9 => array(
"UNIT" => "Millenniums", 
"VALUE" => 1000 * 365 * 24 * 60 * 60 * $power
)
);

foreach($arTime as $arItem) {
if ($time >= $arItem["VALUE"]) {
$result = $time / $arItem["VALUE"];
$result = str_replace(".", ".", strval(round($result, 2))) . " " . $arItem["UNIT"];
break;
}
}
return $result;
}

```

Now, some people might argue that creating these functions is a bad practice, but we disagree. We believe that if something can increase productivity and make our lives easier, then it’s worth it. It’s always a great feeling to say, “Hey boss, I just saved us 10 minutes of coding with my super cool function!”

Of course, we understand that there are potential downsides to using our functions. If we get our hands on a project developed by a different team that never used these functions, we might have a hard time. But we believe that anything that can help us work smarter, not harder, is worth exploring.

So, let’s raise a cup of coffee (or beer, if that’s more your thing) to productivity and making our lives as developers a little easier.

### Stay tune for part 2
------------
## Exerpt
Tired of trying to remember the structure of common PHP function? We’ve got you covered!
## Description
Are you tired of struggling to remember native PHP functions? Check out our suite of functions covering areas like string manipulation, working with HTML and URLs, and array manipulation. Save time and increase productivity as a PHP developer with our time-saving coding tips.
## Media
<img src="media/9b29215e/cover-supereasy-php-functions.jpg" loading="lazy"><br>
<img src="media/1871d4cf/php-functions-1.jpg" loading="lazy"><br>

------------
- **Slug:** supereasy-php-functions
- **Date:** 10/02/2023
- **URL:** [https://phixel.net/en/devdiary/supereasy-php-functions/](https://phixel.net/en/devdiary/supereasy-php-functions/)
- **Short URL:** [https://bit.ly/3mvKRur](https://bit.ly/3mvKRur)
- **Type:** [DevDiary](#devdiary)
- **Hashtags:** #PHPDevelopment, #WebDevelopment, #Coding, #Productivity, #FunctionLibraries, #CodeEfficiency, #PHPFunctions, #PHPLibraries, #SoftwareDevelopment, #Programming, #ProductivityHacks, #ProgrammingTips, #CodeTricks, #WebApps, #DevelopersLife, #CodingSkills, #TechnologyUpdates, #EasyProgramming
- **Emojis:** 🚀🤖💻👨‍💻📈📊💡🔧🛠️☕💻🚀📈👨‍💻👩‍💻🔧💡🤖👌🍻

------------
## Tags
[Code Efficiency](#code-efficiency), [Coding](#coding), [Development](#development), [Function Libraries](#function-libraries), [PHP Development](#php-development), [PHP Functions](#php-functions), [PHP Libraries](#php-libraries), [Productivity](#productivity), [Programming](#programming), [Software Development](#software-development), [Technology](#technology), [Web](#web), [Web Development](#web-development)
