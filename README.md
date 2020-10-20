# Laravel Cutlet Helper
[![GitHub issues](https://img.shields.io/github/issues/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper?style=flat-square)](https://github.com/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper/issues)
[![GitHub stars](https://img.shields.io/github/stars/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper?style=flat-square)](https://github.com/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper?style=flat-square)](https://github.com/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper/network)
[![GitHub license](https://img.shields.io/github/license/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper?style=flat-square)](https://github.com/va1hi9da9sh2ou0rz2ad1eh7/cutlet-helper/blob/master/LICENSE)


### Installation

```

composer require va/cutlet-helper

```

#### Publish Config file

```

php artisan vendor:publish --tag=cutlet-helper

```

#### Helper functions and facades that exists in package

```
1. integerToken($length = 5) : Generate integer token or code

2. stringToken($length = 16, $characters = '2345679acdefghjkmnpqrstuvwxyz') : Generate string token or code

3. digitsToEastern($number) : Covert a Weatern number(English) or digits to Eastern number(Persian or Arabic)

4. isActive($key, $activeClassName = 'active') : Check the route name(string) or route names(array) is avtive or no for css classes

..
```
#### Helper Functions Usage
```
## With Facade format:

CutletHelper::integerToken(length: 10);
CutletHelper::stringToken(length: 32, characters: '2345679acdefghjkmnpqrstuvwxyz');
CutletHelper::digitsToEastern(number: 1375);
CutletHelper::isActive(key: ['posts.index', 'posts.create', 'posts.edit'], activeClassName: 'acive');

## Call a helper function:

integerToken(length: 10)
stringToken(length: 32, characters: '2345679acdefghjkmnpqrstuvwxyz');
digitsToEastern(number: 1375);
isActive(key: ['posts.index', 'posts.create', 'posts.edit'], activeClassName: 'acive');

```

#### Validators that exists in package
- National Code (کد ملی)
- IBAN (شماره شبا)
- Debit Card (شماره کارت بانکی)
- Postal Code (کد پستی)
- Shenase Meli (شناسه ملی)
- Mobile (موبایل)

#### Validators Usage

> national_code
>
>A rule for validating Iranian national code [(How calculated)](https://fa.wikipedia.org/wiki/%DA%A9%D8%A7%D8%B1%D8%AA_%D8%B4%D9%86%D8%A7%D8%B3%D8%A7%DB%8C%DB%8C_%D9%85%D9%84%DB%8C#%D8%AD%D8%B3%D8%A7%D8%A8_%DA%A9%D8%B1%D8%AF%D9%86_%DA%A9%D8%AF_%DA%A9%D9%86%D8%AA%D8%B1%D9%84)
```
return [
    'code' => 'required|national_code'
];

-- OR --

return [
    'code' => ['required', 'national_code']
];

-- OR --

$validatedData = $request->validate([
    'code' => 'national_code',
]);
```

> iban
>
>A rule for validating IBAN (International Bank Account Number) known in Iran as Sheba. [(How calculated)](https://fa.wikipedia.org/wiki/%D8%A7%D9%84%DA%AF%D9%88%D8%B1%DB%8C%D8%AA%D9%85_%DA%A9%D8%AF_%D8%B4%D8%A8%D8%A7#%D8%A7%D9%84%DA%AF%D9%88%D8%B1%DB%8C%D8%AA%D9%85_%DA%A9%D8%AF_%D8%B4%D8%A8%D8%A7)
```
return [
    'account' => 'iban'
];

-- OR --

Add `false` optional parameter after `iban`, If IBAN doesn't begin with `IR`, so the validator will add `IR` as default to the account number:
return [
    'account' => 'iban:false'
];

-- OR --

If you want to validate non Iranian IBAN, add the 2 letters of country code after `false` optional parameter:
return [
    'account' => 'iban:false,DE'
];
```

> debit_card
>
>A rule for validating Iranian debit cards. [(How calculated)](http://www.aliarash.com/article/creditcart/credit-debit-cart.htm)
```
return [
    'code' => 'required|debit_card'
];

-- OR --

return [
    'code' => ['required', 'debit_card']
];

-- OR --

$validatedData = $request->validate([
    'code' => 'debit_card',
]);

-- OR --

You can add an optional parameter if you want to validate a card from a specific bank:
return [
    'code' => 'required|debit_card:bmi'
];

List of the bank codes:

 - bmi (بانک ملی)
 - banksepah (بانک سپه)
 - edbi (بانک توصعه صادرات)
 - bim (بانک صنعت و معدن)
 - bki (بانک کشاورزی)
 - bank-maskan (بانک مسکن)
 - postbank (پست بانک ایران)
 - ttbank (بانک توسعه تعاون)
 - enbank (بانک اقتصاد نوین)
 - parsian-bank (بانک پارسیان)
 - bpi (بانک پاسارگاد)
 - karafarinbank (بانک کارآفرین)
 - sb24 (بانک سامان)
 - sinabank (بانک سینا)
 - sbank (بانک سرمایه)
 - shahr-bank (بانک شهر)
 - bank-day (بانک دی)
 - bsi (بانک صادرات)
 - bankmellat (بانک ملت)
 - tejaratbank (بانک تجارت)
 - refah-bank (بانک رفاه)
 - ansarbank (بانک انصار)
 - mebank (بانک مهر اقتصاد)
```

> postal_code
```
return [
    'code' => 'required|postal_code'
];

--OR--

return [
    'code' => ['required, 'postal_code']
];

--OR--

$validatedData = $request->validate([
    'code' => 'postal_code',
]);
```

> shenase_meli
>
>A rule for validating Iranian shenase meli [(How calculated)](http://www.aliarash.com/article/shenasameli/shenasa_meli.htm)
```
return [
    'code' => 'required|shenase_meli'
];

--OR--

return [
    'code' => ['required, 'shenase_meli']
];

--OR--

$validatedData = $request->validate([
    'code' => 'shenase_meli',
]);
```

> mobile
```
return [
    'mobile' => 'required|mobile'
];

--OR--

return [
    'mobile' => ['required, 'mobile']
];

--OR--

$validatedData = $request->validate([
    'mobile' => 'mobile',
]);
```

#### Requirements:

- PHP v7.0 or above
- Laravel v5.6.0 or above