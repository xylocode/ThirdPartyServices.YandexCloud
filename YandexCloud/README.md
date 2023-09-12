# Yandex.Clould API client library

Unofficial assembly of .proto files for working with the Yandex.Cloud API using the gRPC protocol.

Resources:

- [NuGet](https://www.nuget.org/packages/XyloCode.ThirdPartyServices.YandexCloud)
- [GitHub (source code)](https://github.com/xylocode/ThirdPartyServices.YandexCloud)
- [cloudapi](https://github.com/yandex-cloud/cloudapi) — official .proto files
- Official [documentation](https://cloud.yandex.com/en/docs)

## Yandex.Cloud

A full-fledged cloud platform providing scalable infrastructure, storage, machine learning and development tools to build and enhance digital services and applications.

Developed by Yandex, one of the largest technological companies in the world that builds intelligent products and services.

## Changes to the official code (.proto files)

In the file `yandex\cloud\datatransfer\v1\endpoint\parsers.proto` `message Parser` has been renamed to `Parser1`, renamed dependencies.

## How to use

Before creating a communication channel, you need to understand which endpoint should be used, for this you should refer to the documentation:
[https://cloud.yandex.com/en/docs/api-design-guide/concepts/endpoints](https://cloud.yandex.com/en/docs/api-design-guide/concepts/endpoints)

Also, IAM-Token or service account should be used as a token.

```cs
using Grpc.Core;
using Grpc.Net.Client;
using Yandex.Cloud.API.AI.Translate.V2;

namespace ConsoleApp1
{
    internal class Program
    {
        static void Main(string[] args)
        {
            string token;
            token = @"Bearer t1.XXXXXXXXXXXXXXXXXXXXXXXXXXXXX...";  // for IAM-token
            token = @"Api-Key XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"; // for API-key

            string folderId = "xxxxxxxxxxxxxxxxxxxx";

            using var channel = GrpcChannel.ForAddress("https://translate.api.cloud.yandex.net");
            var ts = new TranslationService.TranslationServiceClient(channel);
            var headers = new Metadata { { "Authorization", token } };
            
            var req1 = new ListLanguagesRequest { FolderId = folderId };
            var res1 = ts.ListLanguages(req1, headers);
            foreach (var item in res1.Languages)
            {
                Console.WriteLine("[{0}]: {1}", item.Code, item.Name);
            }

            var req2 = new TranslateRequest
            {
                FolderId = folderId,
                Format = TranslateRequest.Types.Format.PlainText,
                SourceLanguageCode = "ru",
                TargetLanguageCode = "en",
            };
            req2.Texts.AddRange(new string[] { "Столовая", "Автомастерская", "Торговый центр" });
            var res2 = ts.Translate(req2, headers);
            foreach (var item in res2.Translations)
            {
                Console.WriteLine("{0} / {1}", item.DetectedLanguageCode, item.Text);
            }

            Console.Beep();
            Console.ReadLine();
        }
    }
}
```

## Authors

The following authors have created the source code (.proto files) of "Yandex.Cloud API" published and distributed by YANDEX LLC as the owner:

- Alexander Burmak <alex-burmak@yandex-team.ru>
- Alexander Kirakozov <akirakozov@yandex-team.ru>
- Alexander Klyuev <wizard@yandex-team.ru>
- Alexander Serkov <alxn1@yandex-team.ru>
- Alexey Baranov <baranovich@yandex-team.ru>
- Alexey Zamulla <zamulla@yandex-team.ru>
- Alexey Zasimov <zasimov-a@yandex-team.ru>
- Amy Krishnevsky <krishnevsky@yandex-team.ru>
- Anastasia Karavaeva <dottir@yandex-team.ru>
- Andrey Polyakov <koshachy@yandex-team.ru>
- Damir Makhmutov <yesworld@yandex-team.ru>
- Danila Diugurov <terry@yandex-team.ru>
- David Lanchava <landavid@yandex-team.ru>
- Elena Ilycheva <eilycheva@yandex-team.ru>
- Evgeny Arhipov <arhipov@yandex-team.ru>
- Luba Grinkevich <luba239@yandex-team.ru>
- Maxim Kolganov <manykey@yandex-team.ru>
- Mikhail Goncharov <migelle@yandex-team.ru>
- Nikolay Amelichev <entropia@yandex-team.ru>
- Pavel Fomin <vaccarium@yandex-team.ru>
- Rurik Krylov <rurikk@yandex-team.ru>
- Evgeny Dyukov <secwall@yandex-team.ru>
- Sergey Kanunnikov <skanunnikov@yandex-team.ru>
- Sergey Kiselev <intr13@yandex-team.ru>
- Sergey Sytnik <ssytnik@yandex-team.ru>
- Stanislav Ievlev <sievlev@yandex-team.ru>
- Vasilii Briginets <0x40@yandex-team.ru>
- Vlad Arkhipov <potamus@yandex-team.ru>
- Vladimir Borodin <d0uble@yandex-team.ru>
- Vladimir Skipor <skipor@yandex-team.ru>

## License

MIT License
