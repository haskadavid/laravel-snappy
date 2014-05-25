Laravel snappy package
============

Informations
---

Provider:

```php
'Haska\Snappy\SnappyServiceProvider',
```

Alias:

```php
'PDF' => 'Haska\Snappy\Facades\SnappyPdf',
'Image' => 'Haska\Snappy\Facades\SnappyImage',
```

Config:

```php
php artisan config:publish haska/laravel-snappy
```

## Usage

You can create a new Snappy PDF/Image instance and load a HTML string, file or view name. You can save it to a file, or stream (show in browser) or download.

Using the App container:

    $snappy = App::make('snappy.pdf');
    //To file
    $snappy->generateFromHtml('<h1>Bill</h1><p>You owe me money, dude.</p>', '/tmp/bill-123.pdf');
    $snappy->generate('http://www.github.com', '/tmp/github.pdf'));
    //Or output:
    return new Response(
        $snappy->getOutputFromHtml($html),
        200,
        array(
            'Content-Type'          => 'application/pdf',
            'Content-Disposition'   => 'attachment; filename="file.pdf"'
        )
    );

Using the wrapper:

    $pdf = App::make('snappy.pdf.wrapper');
    $pdf->loadHTML('<h1>Test</h1>');
    return $pdf->stream();

Or use the facade:

    $pdf = PDF::loadView('pdf.invoice', $data);
    return $pdf->download('invoice.pdf');

You can chain the methods:

    return PDF::loadFile('http://www.github.com')->stream('github.pdf');

You can change the orientation and paper size

    PDF::loadHTML($html)->setPaper('a4')->setOrientation('landscape')->setOption('margin-bottom', 0)->save('myfile.pdf')

If you need the output as a string, you can get the rendered PDF with the output() function, so you can save/output it yourself.