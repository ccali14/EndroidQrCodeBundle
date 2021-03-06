Endroid QR Code Bundle
======================

*By [endroid](http://endroid.nl/)*

[![Latest Stable Version](http://img.shields.io/packagist/v/endroid/qrcode-bundle.svg)](https://packagist.org/packages/endroid/qrcode-bundle)
[![Build Status](http://img.shields.io/travis/endroid/EndroidQrCodeBundle.svg)](http://travis-ci.org/endroid/EndroidQrCodeBundle)
[![Latest Stable Version](https://poser.pugx.org/endroid/qrcode-bundle/v/stable.png)](https://packagist.org/packages/endroid/qrcode-bundle)
[![Total Downloads](http://img.shields.io/packagist/dt/endroid/qrcode-bundle.svg)](https://packagist.org/packages/endroid/qrcode-bundle)
[![License](http://img.shields.io/packagist/l/endroid/qrcode-bundle.svg)](https://packagist.org/packages/endroid/qrcode-bundle)

This bundle provides a default controller for generating QR codes using the
Endroid QR Code (endroid/QrCode) library.

[![knpbundles.com](http://knpbundles.com/endroid/EndroidQrCodeBundle/badge-short)](http://knpbundles.com/endroid/EndroidQrCodeBundle)

## Requirements

* Symfony
* Dependencies:
 * [`QrCode`](https://github.com/endroid/QrCode)

## Installation

Use [Composer](https://getcomposer.org/) to install the bundle.

``` bash
$ composer require endroid/qrcode-bundle
```

Then enable the bundle via the kernel.

``` php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new Endroid\Bundle\QrCodeBundle\EndroidQrCodeBundle(),
    );
}
```

## Routing

Add the following section to your routing to be able to handle QR code URLs.
This step can be skipped when you only use data URIs to display your images.

``` yml
EndroidQrCodeBundle:
    resource:   "@EndroidQrCodeBundle/Controller/"
    type:       annotation
    prefix:     /qrcode
```

## Configuration

The default QR code generation parameters can be overridden via the
configuration. All parameters are optional.

### config.yml

```yaml
endroid_qr_code:
    size: 100
    padding: 10
    extension: gif
    error_correction_level: high
    foreground_color: { r: 0, g: 0, b: 0, a: 0 }
    background_color: { r: 255, g: 255, b: 255, a: 0 }
    label: "My label"
    labelFontSize: 16
```

Alpha channel available range is [0, 127] in foreground and background colors.

## Twig extension

The bundle also provides a Twig extension for quickly generating QR code urls.
Optional parameters are extension, size, padding and errorCorrectionLevel. When
a parameter is omitted, the value in the bundle configuration is used.

``` twig
<img src="{{ qrcode_url(message) }}" />
<img src="{{ qrcode_url(message, extension='png') }}" />
<img src="{{ qrcode_url(message, size=150) }}" />
```

You can also use the data URI helper to embed the QR code within your HTML
instead of requiring a separate HTTP request to load your image.

``` twig
<img src="{{ qrcode_data_uri(message, size=200, padding=10) }}" />
```

## Usage

After installation and configuration, QR codes can be generated by appending
the QR code text to the url as mounted, followed by .png, .jpg or .gif.

![QR Code](http://endroid.nl/qrcode/Life%20is%20too%20short%20to%20be%20generating%20QR%20codes.png)

## Versioning

Semantic versioning ([semver](http://semver.org/)) is applied.

## License

This bundle is under the MIT license. For the full copyright and license information, please view the LICENSE file that
was distributed with this source code.
