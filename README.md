# Uppercrust

Inspired by [jsonschema2pojo](https://github.com/joelittlejohn/jsonschema2pojo "jsonschema2pojo"), uppercrust is your trusty companion to generate [Mantle](https://github.com/github/Mantle "Mantle") compatible model files in Objective-C.

Uppercrust generates two header and two implementation files for each of your models. One set is prefixed with an underscore and is meant to be overwritten whenever the JSON schema changes. The files without underscore extends these classes and can be used to add custom functionality and custom mappings and should only be generated once.

## Installation

Install the gem as:

    $ gem install uppercrust

## Usage

    $ uppercrust generate --path {path} --base_only true|false
    
This generate an output folder with all the JSON files mapped to their Objective-C counterparts.

Say for example, you have a model file named 'article.json'. Running uppercrust will then generate 4 files for you:

* _Article.h
* _Article.m
* Article.h
* Article.m

Lets look at the following simple example:

```json
{
    "type":"object",
    "$schema":"http://json-schema.org/draft-03/schema",
    "id":"Article",
    "description":"Result object that represents an article.",
    "required":true,
    "additionalProperties":false,
    "properties":{
        "brand":{
            "type":"string",
            "id":"brand",
            "required":true
        },
        "sku":{
            "type":"string",
            "id":"sku",
            "required":true
        }
    }
}
```

_Article.h:

```objc
// DO NOT EDIT. This file is machine-generated and constantly overwritten.
// Make changes to article.h instead.
//
// Result object that represents an article.

#import <Mantle/Mantle.h>


@interface _Article : MTLModel<MTLJSONSerializing>

@property(nonatomic, copy, readonly) NSString *brand;
@property(nonatomic, copy, readonly) NSString *sku;

@end
```

_Article.m:
```objc
// DO NOT EDIT. This file is machine-generated and constantly overwritten.
// Make changes to Article.m instead.

#import "_Article.h"

@implementation _Article

+ (NSDictionary *)JSONKeyPathsByPropertyKey {
   return @{
       @"brand" : @"brand",
       @"sku" : @"sku"
   };
}


@end
```

Article.h:
```objc
#import "_Article.h"

@interface Article : _Article
@end
```

Article.m:
```objc
#import "Article.h"

@implementation Article

@end
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## TODO

* Add tests!
* Add some special types to the schema since Foundation has a richer vocabulary
* Add the option to prefix the generated class names