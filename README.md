# MvcCore - Extension - Form - Validator - Special

[![Latest Stable Version](https://img.shields.io/badge/Stable-v5.1.3-brightgreen.svg?style=plastic)](https://github.com/mvccore/ext-form-validator-special/releases)
[![License](https://img.shields.io/badge/License-BSD%203-brightgreen.svg?style=plastic)](https://mvccore.github.io/docs/mvccore/5.0.0/LICENSE.md)
![PHP Version](https://img.shields.io/badge/PHP->=5.4-brightgreen.svg?style=plastic)

MvcCore form extension with special text and numeric validators - company ID (EU), company VAT ID (EU), credit card, hexadecimal number, IBAN bank account number, IP address and ZIP code.

## Installation
```shell
composer require mvccore/ext-form-validator-special
```

## Basic Example
```php
$form = (new \MvcCore\Ext\Form($controller))
	->SetId('demo')
	->SetLocale('DE'); // for ZIP validator
...
$yourCreditCard = new \MvcCore\Ext\Forms\Fields\Number();
$yourCreditCard
	->SetName('your_credit_card')
	->SetLabel('Your Credit Card Number:')
	->SetValidators(
		(new \MvcCore\Ext\Forms\Validators\CreditCard)
			-> SetAllowedTypes(
				\MvcCore\Ext\Forms\Validators\CreditCard::AMERICAN_EXPRESS,
				\MvcCore\Ext\Forms\Validators\CreditCard::DISCOVER,
				\MvcCore\Ext\Forms\Validators\CreditCard::MAESTRO,		
				\MvcCore\Ext\Forms\Validators\CreditCard::MASTERCARD,
				\MvcCore\Ext\Forms\Validators\CreditCard::VISA
			)
	);
$yourIp = new \MvcCore\Ext\Forms\Fields\Text([
	'name'		=> 'your_ip',
	'label'		=> 'Your IP Address:',
	'validators'	=> [
		new \MvcCore\Ext\Forms\Validators\Ip([
			'allowIPv4HexFormat'	=> FALSE,
			'allowIPv4BinaryFormat'	=> FALSE,
			'allowIPv6Literals'		=> TRUE,
		])
	],
]);
$yourZipCode = new \MvcCore\Ext\Forms\Fields\Text([
	'name'		=> 'your_zip_code',
	'label'		=> 'Your ZIP code:',
	'validators'	=> ['ZipCode'],
]);
...
$form->AddFields($yourCreditCard, $yourIp, $yourZipCode);
```
