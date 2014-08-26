# PHPWord

This repository is an source code of [PHPWord](http://phpword.codeplex.com/), turned into [Composer](http://getcomposer.org/) package.
This repository is forked from [ferdynator](https://github.com/ferdynator/PHPWord).

## Installation
All you have to do is to [get composer](http://getcomposer.org/download/) and add following lines to your `composer.json`:

        "require": {
           "teqneers/phpword": "*"
        }
        
## Examples

### CantSplit in Tables
Prevents the splitting of a table row if the content does not fit on the page. The whole row moves to a new page. 
See http://msdn.microsoft.com/en-us/library/documentformat.openxml.wordprocessing.cantsplit(v=office.14).aspx

```php
...
$wordTable = $section->addTable('tableStyle');
$wordTable->setCantSplit(true);
...
```

### Usage of tab stops

```php
<?php
require_once '../PHPWord.php';

// New Word Document
$PHPWord = new PHPWord();

$PHPWord->addParagraphStyle('multipleTab', array(
    'tabs' => array(
        new PHPWord_Style_Tab("left", 1550),
        new PHPWord_Style_Tab("center", 3200),
        new PHPWord_Style_Tab("right", 5300)
    )
));

$PHPWord->addParagraphStyle('rightTab', array(
    'tabs' => array(
        new PHPWord_Style_Tab("right", 9090)
    )
));

$PHPWord->addParagraphStyle('centerTab', array(
    'tabs' => array(
        new PHPWord_Style_Tab("center", 4680)
    )
));

// New portrait section
$section = $PHPWord->createSection();

// Add listitem elements
$section->addText("Multiple Tabs:\tOne\tTwo\tThree", NULL, 'multipleTab');
$section->addText("Left Aligned\tRight Aligned", NULL, 'rightTab');
$section->addText("\tCenter Aligned",            NULL, 'centerTab');

// Save File
$objWriter = PHPWord_IOFactory::createWriter($PHPWord, 'Word2007');
$objWriter->save('TabStops.docx');
?>
```
