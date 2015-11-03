# Authorize.Net .Net SDK

[![Build Status](https://travis-ci.org/AuthorizeNet/sdk-dotnet.png?branch=master)]
(https://travis-ci.org/AuthorizeNet/sdk-dotnet)

`PM> Install-Package AuthorizeNet`


## Prerequisites

Requires .NET 3.5 or later and Microsoft&reg; Visual Studio 2008 or 2010; Nunit 2.6.3;


## Installation
To install AuthorizeNet, run the following command in the Package Manager Console:

`PM> Install-Package AuthorizeNet`

## Usage
````csharp
            ApiOperationBase<ANetApiRequest, ANetApiResponse>.MerchantAuthentication = new merchantAuthenticationType()
            {
                name = ApiLoginID,
                ItemElementName = ItemChoiceType.transactionKey,
                Item = ApiTransactionKey,
            };

            var creditCard = new creditCardType
            {
                cardNumber = "4111111111111111",
                expirationDate = "0718"
            };

            var paymentType = new paymentType { Item = creditCard };

            var transactionRequest = new transactionRequestType
            {
                transactionType = transactionTypeEnum.authCaptureTransaction.ToString(),
                amount = 133.45m,
                payment = paymentType
            };

            var request = new createTransactionRequest { transactionRequest = transactionRequest };

            var controller = new createTransactionController(request);
            controller.Execute();

            var response = controller.GetApiResponse();
            
            if (response.messages.resultCode == messageTypeEnum.Ok)
            {
                if (response.transactionResponse != null)
                {
                    Console.WriteLine("Success, Auth Code : " + response.transactionResponse.authCode);
                }
            }
            else
            {
                Console.WriteLine("Error: " + response.messages.message[0].code + "  " + response.messages.message[0].text);
            }
````

## Sample Code
Sample Codes can be found in the following link:

https://github.com/AuthorizeNet/sample-code-csharp

## Building from Source


## Running the Tests
