# vex.mime
MIME library for the [V Programming Language](https://github.com/vlang/v). Inspired from the [mime-types](https://github.com/jshttp/mime-types) JS library.

What does it do? It dentifies the MIME/data types of a file like `application/json`.

## Usage
```v
import mime

// As a workaround, alias the `MimeType` type
type MimeType mime.MimeType

fn main() {
    filepath := './app.json'
    filetype := mime.db.lookup(filepath)

    println(filetype) // application/json
}
```

## API

### mime.lookup(path string)

Lookup the content-type associated with a file.

```v
mime.db.lookup('json')             // 'application/json'
mime.db.lookup('.md')              // 'text/markdown'
mime.db.lookup('file.html')        // 'text/html'
mime.db.lookup('folder/file.js')   // 'application/javascript'
mime.db.lookup('folder/.htaccess') // ''

mime.db.lookup('cats') // ''
```

### mime.content_type(type string)

Create a full content-type header given a content-type or extension.
When given an extension, `mime.db.lookup` is used to get the matching
content-type, otherwise the given content-type is used. Then if the
content-type does not already have a `charset` parameter, `mime.db.charset`
is used to get the default charset and add to the returned content-type.

```v
mime.db.content_type('markdown')  // 'text/x-markdown; charset=utf-8'
mime.db.content_type('file.json') // 'application/json; charset=utf-8'
mime.db.content_type('text/html') // 'text/html; charset=utf-8'
mime.db.content_type('text/html; charset=iso-8859-1') // 'text/html; charset=iso-8859-1'

// from a full path
mime.db.content_type(os.ext('/path/to/file.json')) // 'application/json; charset=utf-8'
```

### mime.extension(type string)

Get the default extension for a content-type.

```v
mime.db.extension('application/octet-stream') // 'bin'
```

### mime.charset(type string)

Lookup the implied default charset of a content-type.

```v
mime.db.charset('text/markdown') // 'UTF-8'
```

## Contributing
1. Fork it (<https://github.com/nedpals/v-mime/fork>)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## License
[MIT](LICENSE)

## Contributors

- [Ned Palacios](https://github.com/nedpals) - creator and maintainer