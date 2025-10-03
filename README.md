<!--
 - SPDX-FileCopyrightText: 2016-2024 Nextcloud GmbH and Nextcloud contributors
 - SPDX-FileCopyrightText: 2013-2016 ownCloud, Inc.
 - SPDX-License-Identifier: AGPL-3.0-or-later
-->
# Nextcloud Server ☁
[![REUSE status](https://api.reuse.software/badge/github.com/nextcloud/server)](https://api.reuse.software/info/github.com/nextcloud/server)
[![codecov](https://codecov.io/gh/nextcloud/server/branch/master/graph/badge.svg)](https://codecov.io/gh/nextcloud/server)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/209/badge)](https://bestpractices.coreinfrastructure.org/projects/209)
[![Design](https://contribute.design/api/shield/nextcloud/server)](https://contribute.design/nextcloud/server)

**A safe home for all your data.**

![](https://raw.githubusercontent.com/nextcloud/screenshots/master/nextcloud-hub-files-25-preview.png)

## Why is this so awesome? 🤩

* 📁 **Access your Data** You can store your files, contacts, calendars, and more on a server of your choosing.
* 🔄 **Sync your Data** You keep your files, contacts, calendars, and more synchronized amongst your devices.
* 🙌 **Share your Data** …by giving others access to the stuff you want them to see or to collaborate with.
* 🚀 **Expandable with hundreds of Apps** ...like [Calendar](https://github.com/nextcloud/calendar), [Contacts](https://github.com/nextcloud/contacts), [Mail](https://github.com/nextcloud/mail), [Video Chat](https://github.com/nextcloud/spreed) and all those you can discover in our [App Store](https://apps.nextcloud.com)
* 🔒 **Security** with our encryption mechanisms, [HackerOne bounty program](https://hackerone.com/nextcloud) and two-factor authentication.

Do you want to learn more about how you can use Nextcloud to access, share, and protect your files, calendars, contacts, communication & more at home and in your organization? [**Learn about all our Features**](https://nextcloud.com/athome/).

## Get your Nextcloud 🚚

- ☑️ [**Simply sign up**](https://nextcloud.com/signup/) at one of our providers either through our website or through the apps directly.
- 🖥 [**Install** a server by yourself](https://nextcloud.com/install/#instructions-server) on your hardware or by using one of our ready-to-use **appliances**
- 📦 Buy one of the [awesome **devices** coming with a preinstalled Nextcloud](https://nextcloud.com/devices/)
- 🏢 Find a [service **provider**](https://nextcloud.com/providers/) who hosts Nextcloud for you or your company

Enterprise? Public Sector or Education user? You may want to have a look into [**Nextcloud Enterprise**](https://nextcloud.com/enterprise/) provided by Nextcloud GmbH.

## Get in touch 💬

* [📋 Forum](https://help.nextcloud.com)
* [👥 Facebook](https://www.facebook.com/nextclouders)
* [🐣 Twitter](https://twitter.com/Nextclouders)
* [🐘 Mastodon](https://mastodon.xyz/@nextcloud)

You can also [get support for Nextcloud](https://nextcloud.com/support)!


## Join the team 👪

There are many ways to contribute, of which development is only one! Find out [how to get involved](https://nextcloud.com/contribute/), including as a translator, designer, tester, helping others, and much more! 😍


### Development setup 👩‍💻

1. 🚀 [Set up your local development environment](https://docs.nextcloud.com/server/latest/developer_manual/getting_started/devenv.html)
2. 🐛 [Pick a good first issue](https://github.com/nextcloud/server/labels/good%20first%20issue)
3. 👩‍🔧 Create a branch and make your changes. Remember to sign off your commits using `git commit -sm "Your commit message"`
4. ⬆ Create a [pull request](https://opensource.guide/how-to-contribute/#opening-a-pull-request) and `@mention` the people from the issue to review
5. 👍 Fix things that come up during a review
6. 🎉 Wait for it to get merged!

Third-party components are handled as git submodules which have to be initialized first. So aside from the regular git checkout invoking `git submodule update --init` or a similar command is needed, for details see Git documentation.

Several apps that are included by default in regular releases such as [First run wizard](https://github.com/nextcloud/firstrunwizard) or [Activity](https://github.com/nextcloud/activity) are missing in `master` and have to be installed manually by cloning them into the `apps` subfolder.

Otherwise, git checkouts can be handled the same as release archives, by using the `stable*` branches. Note they should never be used on production systems.


### Tools we use 🛠

- [👀 BrowserStack](https://browserstack.com) for cross-browser testing
- [🌊 WAVE](https://wave.webaim.org/extension/) for accessibility testing
- [🚨 Lighthouse](https://developers.google.com/web/tools/lighthouse/) for testing performance, accessibility, and more

#### Helpful bots at GitHub :robot:

- Comment on a pull request with `/update-3rdparty` to update the 3rd party submodule. It will update to the last commit of the 3rd party branch named like the PR target.

#### Ignore code style updates in git blame

`git config blame.ignoreRevsFile .git-blame-ignore-revs`

## Contribution guidelines 📜

All contributions to this repository from June 16, 2016, and onward are considered to be
licensed under the AGPLv3 or any later version.

Nextcloud doesn't require a CLA (Contributor License Agreement).
The copyright belongs to all the individual contributors. 
Therefore we recommend that every contributor adds the following line to the [AUTHORS](AUTHORS) file if they made substantial changes to the code:

```
- <your name> <your email address>
```


swagger: '2.0'
info:
  title: vr-bpa-eapi-v1
  description: The experience API is for BPA functionality to retrieve the information from Salesforce
  version: v1
host: api.dxp-dev.dmv.ca.gov
basePath: /vr-bpa-eapi-v1-dev/api/
schemes:
  - https
paths:
  /salvage-vehicle:
    x-amf-displayName: Original Salvage Vehicle Transaction.
    post:
      operationId: Add salvage-vehicle
      description: Create a new salvage-vehicle
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/salvage-vehicle'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /renew-vehicle-registration:
    x-amf-displayName: Renew Vehicle Registration Transaction.
    post:
      operationId: Add renew-vehicle-registration
      description: Create a new renew-vehicle-registration
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/renew-vehicle-registration'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /register-original-vehicle:
    x-amf-displayName: Register Original Vehicle Transaction.
    post:
      operationId: Add register-original-vehicle
      description: Create a new register-original-vehicle
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/register-original-vehicle'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /junk-vehicle-registration:
    x-amf-displayName: Junk Vehicle Registration Transaction.
    post:
      operationId: Add junk-vehicle-registration
      description: Create a new junk-vehicle-registration
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/junk-vehicle-registration'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /transfer-vehicle-ownership:
    x-amf-displayName: Transfer Vehicle Ownership Transaction.
    post:
      operationId: Add transfer-vehicle-ownership
      description: Create a new transfer-vehicle-ownership
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/transfer-vehicle-ownership'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /nonrepairable-certificates:
    x-amf-displayName: Nonrepairable Certificates Transaction.
    post:
      operationId: Add nonrepairable-certificate
      description: Create a new nonrepairable-certificate
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/nonrepairable-certificates'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /new-vessel-registration:
    x-amf-displayName: New Vessel Registration Transaction.
    post:
      operationId: Add new-vessel-registration
      description: Create a new new-vessel-registration
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/new-vessel-registration'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /revived-junk-salvage:
    x-amf-displayName: Revived Junk Salvage Transaction.
    post:
      operationId: Add revived-junk-salvage
      description: Create a new revived-junk-salvage
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/revived-junk-salvage'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /post-fees:
    x-amf-displayName: Original Post Fees Transaction.
    post:
      operationId: Add post-fee
      description: Create a new post-fee
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/post-fees'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /duplicate-title:
    x-amf-displayName: Duplicate Title Transaction.
    post:
      operationId: Add duplicate-title
      description: Create a new duplicate-title
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/duplicate-title'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /original-salvage-certificates:
    x-amf-displayName: Originals Salvage Certificates Transaction.
    post:
      operationId: Add original-salvage-certificate
      description: Create a new original-salvage-certificate
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/original-salvage-certificates'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /non-resident:
    x-amf-displayName: Non Resident Transaction.
    post:
      operationId: Add non-resident
      description: Create a new non-resident
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/non-resident'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /non-original-posting-fees:
    x-amf-displayName: Non Original Posting Fees Transaction.
    post:
      operationId: Add non-original-posting-fee
      description: Create a new non-original-posting-fee
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/non-original-posting-fees'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /vehicle-license-fee-refund:
    x-amf-displayName: Vehicle License Fee Refund Transaction.
    post:
      operationId: Add vehicle-license-fee-refund
      description: Create a new vehicle-license-fee-refund
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/vehicle-license-fee-refund'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /miscellaneous-originals:
    x-amf-displayName: Miscellaneous Originals Transaction.
    post:
      operationId: Add miscellaneous-original
      description: Create a new miscellaneous-original
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/miscellaneous-originals'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /legal-owner-transfer:
    x-amf-displayName: Legal Owner Transfer Transaction.
    post:
      operationId: Add legal-owner-transfer
      description: Create a new legal-owner-transfer
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/legal-owner-transfer'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /retrieve-prior-transaction:
    x-amf-displayName: Retrieve Prior Transaction Transaction.
    post:
      operationId: Add retrieve-prior-transaction
      description: Create a new retrieve-prior-transaction
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/retrieve-prior-transaction'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              citation:
                - bailAmount: 500 USD
                  courtCode: CourtXYZ
                  date: '2023-09-28'
                - bailAmount: 750 USD
                  courtCode: Court123
                  date: '2023-09-26'
              ' prtData ':
                - printData:
                    - allocatedCountyCode: ABC123
                      axlesPropulson: '4'
                      bodyTypeModel: Sedan
                      clearanceInformation: High
                      cylinders: '6'
                      date1StsoldPurchaseDate: '2023-01-15'
                      elpCbFee: $50.00
                      engineNumber: E123456789
                      equipmentNumber: EQ789012
                      expirationDate: '2024-12-31'
                      feeExemptionIndicator: 'No'
                      fleetOperatorNumber: FO123
                      insertCode: IC456
                      licenseNumberPlateFormat: 123-ABC
                      loAddress: 123 Main St
                      loCity: Cityville
                      loName: John Doe
                      loNameOrAddress2NdLine: ''
                      loNameOrAddress3RdLine: ''
                      loZip: '12345'
                      loZip4: '6789'
                      mail: john.doe@example.com
                      makeBuilder: Toyota
                      motivePowerFuelCode: Gasoline
                      paperCode: PC789
                      paperIssueCode: PI567
                      paperIssueDate: '2023-01-10'
                      priorHistoryCode: PH456
                      reel: RE123
                      registrationFee: $100.00
                      ro1StLineName: Auto Repair Shop
                      ro2NdLineNameAddrIndicator: 'Y'
                      ro2NdLineNameAddress: 456 Service Rd
                      ro3RdLineNameAddrIndicator: 'N'
                      ro3RdLineNameAddress: ''
                      ro4ThLineNameAddrIndicatorAN: 'N'
                      ro4ThLineNameAddress: ''
                      roCity: Repairville
                      roCountyCode: XYZ
                      roStreetAddress: 123 Repair St
                      sequenceNumber: '123456789'
                      smogAbatementFee: $20.00
                      specialHandleCode: SH789
                      totalFeesPaid: $170.00
                      typeLicense: Private
                      typeRecordCode: TRC789
                      typeVehicleBodyTypeVesselHull: Sedan
                      unladenWeightVesselLgth: 3500 lbs
                      vehicleLicenseFee: $50.00
                      vinHin: 1HGCM82633A123456
                      vlfClass: Class C
                      weightCodeHullMaterial: Metal
                      weightFee: $30.00
                      yearBuilt: '2023'
                      yearModel: '2023'
                  barcode:
                    widthRatio: 4
                    startPos: '010'
                    readable: 1
                    narrowWidth: 2
                    density: '09'
                    dataLength: '07'
                    data: VEH-01295
                    checkDigit: 1
                    bcType: 1
                    barHeight: 9
              feeTotal: '200.98'
              feePrevPaid: '170'
              feeAdj: '100'
              fee:
                - type: F03
                  amt: '100'
              parkingCitationsTotalDue: '1250.00'
              message: Success
              errorDetails: null
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /preSignedURL:
    x-amf-displayName: Retrieve Pre signed URL for uploaded document.
    get:
      operationId: Add preSignedURL
      description: Create a new preSignedURL
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: true
          in: header
          type: string
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema: {}
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /retrieve-fee-summary:
    x-amf-displayName: Retrieve Fee Summary Transaction.
    post:
      operationId: Add <<resourcePathName | !singularize>>
      description: Create a new <<resourcePathName | !singularize>>
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/retrieve-fee-summary'
      responses:
        '200':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            example:
              errorDetails: null
              finBusinessDate: '2020-01-01'
              finGrandTotal: '1024.23'
              financial:
                - tnNumberTrans: '12'
                  finSubTotal: '123'
                  finBpId: 43AS
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /verifyInventory:
    x-amf-displayName: Verify Inventory Transaction.
    post:
      operationId: Add <<resourcePathName | !singularize>>_1
      description: Create a new <<resourcePathName | !singularize>>
      consumes:
        - application/json
      produces:
        - application/json
      parameters:
        - name: x-correlation-id
          description: A unique correlationID for each transaction
          required: true
          in: header
          type: string
          minLength: 1
        - name: dmv_source
          description: Source of request.
          required: true
          in: header
          type: string
          minLength: 1
        - name: transactionId
          description: A unique Id for transaction.
          required: false
          in: header
          type: string
        - x-amf-mediaType: application/json
          in: body
          name: generated
          schema:
            $ref: '#/definitions/verifyInventory'
      responses:
        '200':
          description: ''
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/verifyInventorySample'
        '400':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '401':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '403':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '404':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '405':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '406':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '415':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
        '500':
          description: ''
          headers:
            x-correlation-id:
              x-amf-required: true
              description: Unique Id from FLSP request
              type: string
            transactionId:
              x-amf-required: false
              description: Unique Id created by DMV for each transaction
              type: string
          x-amf-mediaType: application/json
          schema:
            $ref: '#/definitions/error-message'
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
  /health-check:
    get:
      operationId: health-check
      description: ''
      produces:
        - application/json
      responses:
        '200':
          description: 'null'
          x-amf-mediaType: application/json
          schema:
            example:
              healthy: true
              name: your-api-name-here
              version: v1
              env: dev
              description: api is healthy
              systemInfo:
                - name: sfdc
                  status: connected OK
            type: object
            required:
              - healthy
              - name
              - version
              - env
              - description
              - systemInfo
            properties:
              healthy:
                example: true
                type: boolean
              name:
                type: string
              version:
                type: string
              env:
                type: string
              description:
                type: string
              systemInfo:
                type: array
                items:
                  type: object
                  required:
                    - name
                    - status
                  properties:
                    name:
                      description: name of the downstream system or API this API is connecting to
                      example: sfdc
                      type: string
                    status:
                      example: connected OK
                      type: string
        '500':
          description: health-check information
          x-amf-mediaType: application/json
          schema:
            example:
              healthy: false
              name: your-api-name-here
              version: v1
              env: dev
              description: api is not healthy
              systemInfo:
                - name: sfdc
                  status: 'error: CONN_REFUSED with 10.4.45.6'
            type: object
            required:
              - healthy
              - name
              - version
              - env
              - description
              - systemInfo
            properties:
              healthy:
                example: false
                type: boolean
              name:
                type: string
              version:
                type: string
              env:
                type: string
              description:
                type: string
              systemInfo:
                type: array
                items:
                  type: object
                  required:
                    - name
                    - status
                  properties:
                    name:
                      description: name of the downstream system or API this API is connecting to
                      example: sfdc
                      type: string
                    status:
                      example: error-message-here
                      type: string
      security:
        - securities-fragment.oauth_2_0_azuread_client_cred: []
definitions:
  salvage-vehicle:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      clearingIndc: 'N'
      wreckOrLossDate: '2024-02-23'
      dealerDismantlerNumber: 1
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      lienholderNameOnRecord: 'Y'
      make: ACUR
      inventoryCode:
        - '012'
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      nonRepairableReasonCode: B
      newPlateNumber: R43E345R
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      vinHin: JH4DB7560SS004122
      lawEnforcement: '00'
      lastTransferDate: '2024-01-01'
      numOfTransfers: 2
      ownerNameOnRecord: ER4
      ownershipCertIssueDate: '2024-01-01'
      priorPlateWithOwnerDisp: L
      priorHistoryIndc: T
      duplicateOwnershipCert: E
      duplicateSalvageCertIndc: E
      odometer: 2
      odometerCode: '68'
      odometerUnit: K
      transCode: S
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      fuelType: S
      transactionDate: '2024-01-01'
    type: object
    required:
      - clearingIndc
      - wreckOrLossDate
      - feeAcceptanceIndc
      - firstPartnerId
      - secondPartnerId
      - lastTransferDate
      - numOfTransfers
      - ownerNameOnRecord
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      wreckOrLossDate:
        example: '2024-02-23'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      nonRepairableReasonCode:
        $ref: '#/definitions/nonRepairableReasonCode'
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      lastTransferDate:
        example: '2024-01-01'
        type: string
        format: date
      numOfTransfers:
        example: 2
        type: integer
        minimum: 1
        maximum: 9
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      duplicateOwnershipCert:
        example: E
        type: string
        minLength: 1
        maxLength: 1
      duplicateSalvageCertIndc:
        example: E
        type: string
        minLength: 1
        maxLength: 1
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      transCode:
        $ref: '#/definitions/transCode'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      tnDate:
        example: '2024-01-01'
        type: string
        format: date
  error-message:
    x-amf-examples:
      example_2:
        success: false
        source: IVR
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 405
            errorType: APIKIT:METHOD_NOT_ALLOWED
            errorMessage: The following request failed with a exception
            errorDescription: ''
      amf_example_1:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 406
            errorType: APIKIT:NOT_ACCEPTABLE
            errorMessage: The following request failed with a exception
            errorDescription: ''
      example_1:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 401
            errorType: APIKIT:UNAUTHORIZED
            errorMessage: Token has been revoked
            errorDescription: ''
      amf_example_2:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 500
            errorType: APIKIT:INTERNAL_SERVER_ERROR
            errorMessage: The following request failed with a exception
            errorDescription: ''
      amf_example_4:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 400
            errorType: APIKIT:BAD_REQUEST
            errorMessage: The following request failed with a exception
            errorDescription: ''
      example_0:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 403
            errorType: APIKIT:FORBIDDEN
            errorMessage: Bad OAuth request (wrong client-id/secret, scopes etc)
            errorDescription: ''
      amf_example_3:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 404
            errorType: APIKIT:NOT_FOUND
            errorMessage: The following request failed with a exception
            errorDescription: ''
      example_3:
        success: false
        source: BPA
        target: Salesforce
        correlationId: 8c670a58-a763-4ed6-819f-2ad3e3148e6d
        identifier: b6bca390-b1df-11ed-afa1-0242ac120002
        timeStamp: '2023-03-13T09:34:15'
        message: ''
        errorDetails:
          - errorCode: 415
            errorType: APIKIT:UNSUPPORTED_MEDIA_TYPE
            errorMessage: The following request failed with a exception
            errorDescription: ''
    type: object
    required:
      - errorDetails
    properties:
      success:
        type: boolean
      source:
        type: string
      target:
        type: string
      correlationId:
        type: string
      identifier:
        type: string
      timestamp:
        type: string
      message:
        type: string
      errorDetails:
        type: array
        items:
          type: object
          additionalProperties: true
          properties:
            code:
              type: number
            type:
              type: string
            text:
              type: string
            description:
              type: string
  renew-vehicle-registration:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dateFeesReceived: '2024-01-01'
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fhvutCode: F
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inventoryCode:
        - '012'
      inspSmog: 'Y'
      lesseeAddressIndc: D
      make: ACUR
      metalTab: 'Y'
      newPlateNumber: R43E345R
      organizationSymbol: V00
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: 43E
      plateWithOwnerName: SAM
      plateWithOwnerReassign: 'Y'
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      situsAddress: 123 MAIN ST
      situsCity: CA
      situsCountyCode: 12
      stickerNumber: 123E
      transactionDate: '2024-01-01'
      typeLicenseCode: '11'
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      arbProof: 'Y'
      certNonOperationDate: '2024-02-23'
      certNonOperationIndc: S
      dupReg: S
      expirationDate: '2024-01-01'
      insuranceVerification: 'N'
      musselFee: 'Y'
      ownerNameOnRecord: ER4
      priorPlateWithOwnerDisp: L
      substitutePlate: '1'
      substituteSticker: '1'
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
    type: object
    required:
      - feeAcceptanceIndc
      - firstPartnerId
      - secondPartnerId
      - vinHin
      - expirationDate
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      inspSmog:
        $ref: '#/definitions/inspSmog'
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        example: 43E
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        example: SAM
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 12
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      tnDate:
        example: '2024-01-01'
        type: string
        format: date
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      arbProof:
        $ref: '#/definitions/arbProof'
      certNonOperationDate:
        example: '2024-02-23'
        type: string
        format: date
      certNonOperationIndc:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      dupReg:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      expirationDate:
        example: '2024-01-01'
        type: string
        format: date
      insuranceVerification:
        $ref: '#/definitions/insuranceVerification'
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      substitutePlate:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      substituteSticker:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
  register-original-vehicle:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      bodyTypeModel: SU
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dateFeesReceived: '2024-02-23'
      dealerDismantlerNumber: 1
      datePurchased: '2024-02-23'
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fhvutCode: F
      fileCode: '2'
      firstPartnerId: V15
      fuelType: S
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inventoryCode:
        - '012'
        - '123'
      lawEnforcement: '00'
      lesseeAddressIndc: '4'
      make: ACUR
      metalTab: 'Y'
      modelYr: 2024
      newPlateNumber: 3DR43ER
      numAxles: 4
      odometer: 2
      odometerCode: '68'
      odometerUnit: K
      organizationSymbolCode: V00
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: '33'
      plateWithOwnerName: '2'
      plateWithOwnerReassign: 'Y'
      printTitle: 'Y'
      purchasePrice: 1
      rdfCode:
        - '0'
        - '2'
        - A
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      reportOfSaleNum: '2321E322'
      secondPartnerId: BM
      situsAddress: '1'
      situsCity: CA
      situsCountyCode: 0
      stickerNumber: AWW
      transactionDate: '2024-02-23'
      typeLicenseCode: '11'
      unladenWgt: 1
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      yearFirstSold: 2023
      lienholderName:
        - codeDlnCurr: 2W23E221
          nameTxt: QW
          typeIndc: '1'
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SD
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SA
          typeIndc: '1'
          codeDlnCurr: ASAS232W
    type: object
    required:
      - dealerDismantlerNumber
      - datePurchased
      - feeAcceptanceIndc
      - firstPartnerId
      - printTitle
      - purchasePrice
      - secondPartnerId
      - typeLicenseCode
      - yearFirstSold
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesReceived:
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      lesseeAddressIndc:
        type: string
        minLength: 1
        maxLength: 1
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      newPlateNumber:
        type: string
        minLength: 7
        maxLength: 8
      numAxles:
        example: 4
        type: integer
        minimum: 1
        maximum: 9
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      printTitle:
        $ref: '#/definitions/printTitle'
      purchasePrice:
        type: number
        minimum: 1
        maximum: 9999999
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      reportOfSaleNum:
        type: string
        minLength: 8
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      tnDate:
        type: string
        format: date
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        type: number
        minimum: 1
        maximum: 99999
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
  junk-vehicle-registration:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dealerDismantlerNumber: 1
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      lienholderNameOnRecord: 'Y'
      make: ACUR
      priorUseTax: 23
      planNonOper: C
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      certNonOperationDate: '2024-02-23'
      certNonOperationIndc: S
      costValue: 2
      lastTransferDate: '2024-02-23'
      lengthInches: 22
      musselFee: 'Y'
      numOfTransfers: 2
      ownerNameOnRecord: ER4
      ownershipCertIssueDate: '2024-01-01'
      priorPlateWithOwnerDisp: L
      repossessionDate: '2024-01-01'
      transCode: J
      transactionDate: '2024-01-01'
      fuelType: S
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
    type: object
    required:
      - feeAcceptanceIndc
      - firstPartnerId
      - secondPartnerId
      - vinHin
      - lastTransferDate
      - numOfTransfers
      - ownerNameOnRecord
      - transCode
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      priorUseTax:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      planNonOper:
        $ref: '#/definitions/planNonOper'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      certNonOperationDate:
        example: '2024-02-23'
        type: string
        format: date
      certNonOperationIndc:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      costValue:
        example: 2
        type: number
        minimum: 1
        maximum: 9999999
      lastTransferDate:
        example: '2024-02-23'
        type: string
        format: date
      lengthInches:
        example: 22
        type: number
        minimum: 0
        maximum: 99
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      numOfTransfers:
        example: 2
        type: integer
        minimum: 1
        maximum: 9
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      repossessionDate:
        example: '2024-01-01'
        type: string
        format: date
      transCode:
        $ref: '#/definitions/jnkTransCode'
      tnDate:
        example: '2024-01-01'
        type: string
        format: date
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
  transfer-vehicle-ownership:
    example:
      accountNumber: qwe
      situsAddress: 123 MAIN ST
      situsCity: CA
      situsCountyCode: 12
      rdfCode:
        - '2'
      inspSmog: 'Y'
      clearingIndc: 'N'
      odometerCode: '68'
      dealerDismantlerNumber: 1
      firstPartnerId: V15
      plateWithOwnerLicense: 43E
      plateWithOwnerFileCode: L
      plateWithOwnerName: SAM
      organizationSymbol: V00
      plateWithOwnerAssign: 'Y'
      plateWithOwnerReassign: 'Y'
      reportOfSaleNum: 212WE34R
      ownershipCertIssueDate: '2024-01-01'
      retainPlateWithOwner: 'Y'
      metalTab: 'Y'
      inspect: C
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lesseeChangeOnlyIndc: 'Y'
      lesseeAddressIndc: D
      lienholderName:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      lienholderNameOnRecord: 'Y'
      odometer: 2
      odometerUnit: K
      dateFeesReceived: '2024-01-01'
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      ownerNameOnRecord: ER4
      planNonOper: C
      certNonOperationIndc: S
      rdfIndicator: 'Y'
      certificationIndc: C
      expirationDate: '2024-02-23'
      newPlateNumber: R43E345R
      stickerNumber: 123E
      dupOwnershipCert: S
      certificationDate: '2024-02-23'
      vlfWgtExempt: 'Y'
      priorHistoryIndc: T
      fileCode: '1'
      regPlateNumber: 2VUB901
      typeLicenseCode: '11'
      repossessionDate: '2024-01-01'
      priorPlateWithOwnerDisp: L
      certNonOperationDate: '2024-02-23'
      printTitle: 'Y'
      numOfTransfers: 2
      secondPartnerId: BM
      substitutePlate: '1'
      substituteSticker: '1'
      feeAcceptanceIndc: 'N'
      musselFee: 'Y'
      equipNum: '12'
      allocatedCounty: '19'
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inventoryCode:
        - '012'
      priorUseTax: 23
      make: ACUR
      lastTransferDate: '2024-02-23'
      useTaxReclassIndc: D
      lengthInches: 22
      purchasePrice: 12.34
      dealerInventoryDate: '2024-02-23'
      costValue: 2
      lawEnforcement: '00'
      fhvutCode: F
      vinHin: JH4DB7560SS004122
      arbProof: 'Y'
      fuelType: S
      transactionDate: '2024-02-23'
    type: object
    required:
      - clearingIndc
      - firstPartnerId
      - ownershipCertIssueDate
      - ownerAddress
      - ownerNameOnRecord
      - expirationDate
      - printTitle
      - numOfTransfers
      - secondPartnerId
      - feeAcceptanceIndc
      - lastTransferDate
      - useTaxReclassIndc
      - purchasePrice
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 12
        type: integer
        minimum: 0
        maximum: 99
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      inspSmog:
        $ref: '#/definitions/inspSmog'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      odometerCode:
        $ref: '#/definitions/odometerCode'
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      plateWithOwnerLicense:
        example: 43E
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerName:
        example: SAM
        type: string
        minLength: 1
        maxLength: 27
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      reportOfSaleNum:
        example: 212WE34R
        type: string
        minLength: 8
        maxLength: 8
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      retainPlateWithOwner:
        $ref: '#/definitions/retainPlateWithOwner'
      metalTab:
        $ref: '#/definitions/metalTab'
      inspect:
        $ref: '#/definitions/inspect'
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      lesseeChangeOnlyIndc:
        $ref: '#/definitions/lesseeChangeOnlyIndc'
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      planNonOper:
        $ref: '#/definitions/planNonOper'
      certNonOperationIndc:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      expirationDate:
        example: '2024-02-23'
        type: string
        format: date
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      dupOwnershipCert:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      repossessionDate:
        example: '2024-01-01'
        type: string
        format: date
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      certNonOperationDate:
        example: '2024-02-23'
        type: string
        format: date
      printTitle:
        $ref: '#/definitions/printTitle'
      numOfTransfers:
        example: 2
        type: integer
        minimum: 1
        maximum: 9
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      substitutePlate:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      substituteSticker:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      priorUseTax:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      lastTransferDate:
        example: '2024-02-23'
        type: string
        format: date
      useTaxReclassIndc:
        $ref: '#/definitions/useTaxReclassIndc'
      lengthInches:
        example: 22
        type: number
        minimum: 0
        maximum: 99
      purchasePrice:
        example: 12.34
        type: number
        minimum: 1
        maximum: 9999999
      dealerInventoryDate:
        example: '2024-02-23'
        type: string
        format: date
      costValue:
        example: 2
        type: number
        minimum: 1
        maximum: 9999999
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      arbProof:
        $ref: '#/definitions/arbProof'
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      tnDate:
        example: '2024-02-23'
        type: string
        format: date
  nonrepairable-certificates:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      asteriskYear: 2024
      bodyTypeModel: SU
      clearingIndc: 'N'
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      inventoryCode:
        - '012'
      make: ACUR
      modelYr: 2024
      nonRepairableReasonCode: S
      numAxles: 4
      priorHistoryIndc: T
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      unladenWgt: 23
      vinHin: JH4DB7560SS004122
      yearFirstSold: 2023
      costValue: 2
      datePurchased: '2024-02-23'
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      wreckOrLossDate: '2024-02-23'
      lastStateReg: E3
      outOfStateTitleNum: '23'
      outOfStateTitleSurrender: 'Y'
      yearRegistered: 34
    type: object
    required:
      - bodyTypeModel
      - clearingIndc
      - feeAcceptanceIndc
      - firstPartnerId
      - secondPartnerId
      - typeLicenseCode
      - yearFirstSold
      - datePurchased
      - ownerAddress
      - wreckOrLossDate
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      asteriskYear:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      nonRepairableReasonCode:
        $ref: '#/definitions/nonRepairableReasonCode'
      numAxles:
        example: 4
        type: integer
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      costValue:
        example: 2
        type: number
        minimum: 1
        maximum: 9999999
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      wreckOrLossDate:
        example: '2024-02-23'
        type: string
        format: date
      lastStateReg:
        example: E3
        type: string
        minLength: 2
        maxLength: 2
      outOfStateTitleNum:
        example: '23'
        type: string
        minLength: 1
        maxLength: 14
      outOfStateTitleSurrender:
        $ref: '#/definitions/outOfStateTitleSurrender'
      yearRegistered:
        example: 34
        type: integer
        minimum: 0
        maximum: 9999
  new-vessel-registration:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      clearingIndc: 'N'
      dateFeesDue: '2024-01-01'
      dateFeesReceived: '2024-01-01'
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      inventoryCode:
        - '012'
      inspSmog: 'Y'
      lesseeAddressIndc: D
      lienholderName:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      modelYr: 2024
      newPlateNumber: R43E345R
      priorUseTax: 23
      purchasePrice: 12.34
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      situsAddress: 123 MAIN ST
      situsCity: CA
      situsCountyCode: 12
      stickerNumber: 123E
      typeLicenseCode: '11'
      useTaxIndicator: 'Y'
      vinHin: BUJ13889J516
      arbProof: 'Y'
      builder: ASDWEDES
      datePurchased: '2024-02-23'
      hullMaterial: A
      lengthFeet: 22
      lengthInches: 22
      monthBuilt: 2
      musselFee: 'Y'
      nonResident: 'Y'
      propulsion: A
      vesselType: X
      yearBuilt: 34
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      make: ACUR
    type: object
    required:
      - clearingIndc
      - dateFeesDue
      - feeAcceptanceIndc
      - firstPartnerId
      - fuelType
      - inspSmog
      - lienholderName
      - modelYr
      - purchasePrice
      - secondPartnerId
      - typeLicenseCode
      - useTaxIndicator
      - vinHin
      - builder
      - datePurchased
      - hullMaterial
      - lengthFeet
      - lengthInches
      - monthBuilt
      - propulsion
      - vesselType
      - yearBuilt
      - ownerAddress
      - ownerInfo
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesDue:
        example: '2024-01-01'
        type: string
        format: date
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      inspSmog:
        $ref: '#/definitions/inspSmog'
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      priorUseTax:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      purchasePrice:
        example: 12.34
        type: number
        minimum: 1
        maximum: 9999999
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 12
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      useTaxIndicator:
        $ref: '#/definitions/useTaxIndicator'
      vinHin:
        example: BUJ13889J516
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 12
      arbProof:
        $ref: '#/definitions/arbProof'
      builder:
        example: ASDWEDES
        type: string
        minLength: 1
        maxLength: 9
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      hullMaterial:
        $ref: '#/definitions/hullMaterial'
      lengthFeet:
        example: 22
        type: number
        minimum: 0
        maximum: 999
      lengthInches:
        example: 22
        type: number
        minimum: 0
        maximum: 99
      monthBuilt:
        example: 2
        type: integer
        minimum: 1
        maximum: 12
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      nonResident:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      propulsion:
        $ref: '#/definitions/propulsion'
      vesselType:
        $ref: '#/definitions/vesselType'
      yearBuilt:
        example: 34
        type: integer
        minimum: 0
        maximum: 9999
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
  revived-junk-salvage:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      asteriskYear: 2024
      bodyTypeModel: SU
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dateFeesDue: '2024-01-01'
      dateFeesReceived: '2024-01-01'
      dealerDismantlerNumber: 1
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fhvutCode: F
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inventoryCode:
        - '012'
      inspSmog: 'Y'
      lawEnforcement: '00'
      lesseeAddressIndc: D
      lienholderName:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      make: ACUR
      metalTab: 'Y'
      modelYr: 2024
      newPlateNumber: R43E345R
      numAxles: 4
      odometer: 2
      odometerCode: '68'
      odometerUnit: K
      organizationSymbol: V00
      priorUseTax: 23
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: 43E
      plateWithOwnerName: SAM
      plateWithOwnerReassign: 'Y'
      purchasePrice: 12.34
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      reportOfSaleNum: 212WE34R
      secondPartnerId: BM
      situsAddress: 123 MAIN ST
      situsCity: CA
      situsCountyCode: 12
      stickerNumber: 123E
      typeLicenseCode: '11'
      unladenWgt: 23
      useTaxIndicator: 'Y'
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      yearFirstSold: 2023
      arbProof: 'Y'
      inspect: C
      junkSalvage: S
      outOfStateServiceFee: 'Y'
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
    type: object
    required:
      - bodyTypeModel
      - clearingIndc
      - dateFeesDue
      - feeAcceptanceIndc
      - firstPartnerId
      - fuelType
      - modelYr
      - secondPartnerId
      - typeLicenseCode
      - useTaxIndicator
      - yearFirstSold
      - inspect
      - junkSalvage
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      asteriskYear:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesDue:
        example: '2024-01-01'
        type: string
        format: date
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      inspSmog:
        $ref: '#/definitions/inspSmog'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      numAxles:
        example: 4
        type: integer
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      priorUseTax:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        example: 43E
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        example: SAM
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      purchasePrice:
        example: 12.34
        type: number
        minimum: 1
        maximum: 9999999
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      reportOfSaleNum:
        example: 212WE34R
        type: string
        minLength: 8
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 2
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      useTaxIndicator:
        $ref: '#/definitions/useTaxIndicator'
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      arbProof:
        $ref: '#/definitions/arbProof'
      inspect:
        $ref: '#/definitions/inspect'
      junkSalvage:
        $ref: '#/definitions/junkSalvage'
      outOfStateServiceFee:
        $ref: '#/definitions/outOfStateServiceFee'
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
  post-fees:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      amountToBePosted: 2
      clearingIndc: 'N'
      datePurchased: '2024-02-23'
      dealerDismantlerNumber: 1
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      make: ACUR
      rdfIndicator: 'Y'
      secondPartnerId: BM
      transactionDate: '2024-01-01'
      vinHin: JH4DB7560SS004122
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
    type: object
    required:
      - datePurchased
      - dealerDismantlerNumber
      - feeAcceptanceIndc
      - fileCode
      - firstPartnerId
      - secondPartnerId
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      amountToBePosted:
        example: 2
        type: integer
        minimum: 1
        maximum: 99999999
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      tnDate:
        type: string
        format: date
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
  duplicate-title:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      arbProof: 'Y'
      certNonOperationDate: '2024-02-23'
      certNonOperationIndc: S
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dateFeesReceived: '2024-02-23'
      equipNum: 1DR4
      expirationDate: '2024-02-23'
      feeAcceptanceIndc: 'N'
      fhvutCode: F
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inspSmog: 'Y'
      insuranceIndicator: 'Y'
      inventoryCode:
        - '012'
      lengthInches: 22
      lesseeAddressIndc: D
      lienholderNameOnRecord: 'Y'
      make: ACUR
      metalTab: 'Y'
      musselFee: 'Y'
      newPlateNumber: R43E345R
      organizationSymbol: V00
      ownerNameOnRecord: ER4
      ownershipCertIssueDate: '2024-01-01'
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: 43E
      plateWithOwnerName: SAM
      plateWithOwnerReassign: 'Y'
      printTitle: 'Y'
      priorPlateWithOwnerDisp: L
      rdfCode: []
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      situsAddress: 123 MAIN ST
      situsCity: CA
      situsCountyCode: 12
      stickerNumber: 123E
      substitutePlate: '1'
      substituteSticker: '1'
      typeLicenseCode: '11'
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
    type: object
    required:
      - expirationDate
      - feeAcceptanceIndc
      - firstPartnerId
      - ownerNameOnRecord
      - ownershipCertIssueDate
      - secondPartnerId
      - vinHin
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      arbProof:
        $ref: '#/definitions/arbProof'
      certNonOperationDate:
        example: '2024-02-23'
        type: string
        format: date
      certNonOperationIndc:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      expirationDate:
        example: '2024-02-23'
        type: string
        format: date
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inspSmog:
        $ref: '#/definitions/inspSmog'
      insuranceIndicator:
        $ref: '#/definitions/insuranceIndicator'
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      lengthInches:
        example: 22
        type: number
        minimum: 0
        maximum: 99
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        example: 43E
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        example: SAM
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      printTitle:
        $ref: '#/definitions/printTitle'
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 12
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      substitutePlate:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      substituteSticker:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
  original-salvage-certificates:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      asteriskYear: 2024
      bodyTypeModel: SU
      clearingIndc: 'N'
      dealerDismantlerNumber: 1
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      fuelType: S
      inventoryCode:
        - '012'
      lawEnforcement: '00'
      make: ACUR
      modelYr: 2024
      numAxles: 4
      odometer: 2
      odometerCode: '68'
      odometerUnit: K
      priorHistoryIndc: T
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      unladenWgt: 23
      vinHin: JH4DB7560SS004122
      yearFirstSold: 2023
      costValue: 2
      datePurchased: '2024-02-23'
      lastStateReg: E3
      outOfStateTitleNum: '23'
      outOfStateTitleSurrender: 'Y'
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      wreckOrLossDate: '2024-02-23'
      yearRegistered: 34
    type: object
    required:
      - bodyTypeModel
      - clearingIndc
      - feeAcceptanceIndc
      - firstPartnerId
      - secondPartnerId
      - yearFirstSold
      - datePurchased
      - wreckOrLossDate
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      asteriskYear:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      numAxles:
        example: 4
        type: integer
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        example: 23
        type: number
        minimum: 1
        maximum: 99999
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      costValue:
        example: 2
        type: number
        minimum: 1
        maximum: 9999999
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      lastStateReg:
        example: E3
        type: string
        minLength: 2
        maxLength: 2
      outOfStateTitleNum:
        example: '23'
        type: string
        minLength: 1
        maxLength: 14
      outOfStateTitleSurrender:
        $ref: '#/definitions/outOfStateTitleSurrender'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      wreckOrLossDate:
        example: '2024-02-23'
        type: string
        format: date
      yearRegistered:
        example: 34
        type: integer
        minimum: 0
        maximum: 9999
  non-resident:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      bodyTypeModel: SU
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dateFeesReceived: '2024-02-23'
      datePurchased: '2024-02-23'
      dealerDismantlerNumber: 1
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fhvutCode: F
      fileCode: '2'
      firstPartnerId: V15
      fuelType: S
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inventoryCode:
        - '0E4'
        - '1E3'
      lawEnforcement: '00'
      lesseeAddressIndc: '4'
      make: ACUR
      metalTab: 'Y'
      modelYr: 2024
      newPlateNumber: 2SR4321
      numAxles: 4
      odometer: 2582
      odometerCode: '68'
      odometerUnit: K
      organizationSymbol: V00
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: SD
      plateWithOwnerName: SAM
      plateWithOwnerReassign: 'Y'
      printTitle: 'N'
      purchasePrice: 12
      rdfCode:
        - '0'
        - '2'
        - A
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      reportOfSaleNum: 1WS23DFE
      secondPartnerId: BM
      situsAddress: SAD
      situsCity: CA
      situsCountyCode: 0
      stickerNumber: '1'
      transactionDate: '2024-02-23'
      typeLicenseCode: '11'
      unladenWgt: 13
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      yearFirstSold: 2023
      outOfStateLicenseNum: '1'
      dateFeesDue: '2024-02-23'
      yearRegistered: 2024
      lastStateReg: 4R
      outOfStateTitleSurrender: 'Y'
      issueCaOwnershipCert: 'Y'
      useTaxIndicator: 'Y'
      outOfStateTitleNum: A
      lienholderName:
        - nameTxt: SA
          typeIndc: '1'
          codeDlnCurr: ASAS232W
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: MAIN
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: MAIN
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: MAIN
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SA
          typeIndc: '1'
          codeDlnCurr: ASAS232W
    type: object
    required:
      - bodyTypeModel
      - clearingIndc
      - feeAcceptanceIndc
      - firstPartnerId
      - fuelType
      - make
      - modelYr
      - printTitle
      - purchasePrice
      - secondPartnerId
      - typeLicenseCode
      - vinHin
      - yearFirstSold
      - outOfStateLicenseNum
      - dateFeesDue
      - yearRegistered
      - lastStateReg
      - outOfStateTitleSurrender
      - issueCaOwnershipCert
      - useTaxIndicator
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesReceived:
        example: '2024-02-23'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fileCode:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      lesseeAddressIndc:
        type: string
        minLength: 1
        maxLength: 1
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      newPlateNumber:
        type: string
        minLength: 7
        maxLength: 8
      numAxles:
        example: 4
        type: number
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      printTitle:
        $ref: '#/definitions/printTitle'
      purchasePrice:
        type: number
        minimum: 1
        maximum: 9999999
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      reportOfSaleNum:
        type: string
        minLength: 8
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        type: number
        minimum: 1
        maximum: 99999
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      outOfStateLicenseNum:
        type: string
        minLength: 1
        maxLength: 8
      dateFeesDue:
        example: '2024-01-01'
        type: string
        format: date
      yearRegistered:
        type: integer
        minimum: 0
        maximum: 9999
      lastStateReg:
        type: string
        minLength: 2
        maxLength: 2
      outOfStateTitleSurrender:
        $ref: '#/definitions/outOfStateTitleSurrender'
      issueCaOwnershipCert:
        $ref: '#/definitions/issueCaOwnershipCert'
      useTaxIndicator:
        $ref: '#/definitions/useTaxIndicator'
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      asteriskYear:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      inspSmog:
        $ref: '#/definitions/inspSmog'
      outOfStateTitleNum:
        type: string
        minLength: 1
        maxLength: 14
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      priorUseTax:
        type: number
        minimum: 1
        maximum: 99999
  non-original-posting-fees:
    example:
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      ownershipCertIssueDate: '2024-01-01'
      firstPartnerId: V15
      datePurchased: '2024-02-23'
      dealerDismantlerNumber: 1
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      fileCode: '1'
      ownerNameOnRecord: ER4
      rdfIndicator: 'Y'
      expirationDate: '2024-02-23'
      amountToBePosted: 2
      secondPartnerId: BM
      allocatedCounty: '19'
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      lienholderNameOnRecord: 'Y'
      make: ACUR
      vinHin: JH4DB7560SS004122
      accountNumber: qwe
      changeRoData: 'N'
      clearingIndc: 'N'
      regPlateNumber: 2VUB901
    type: object
    required:
      - firstPartnerId
      - dealerDismantlerNumber
      - ownerAddress
      - fileCode
      - ownerNameOnRecord
      - expirationDate
      - amountToBePosted
      - secondPartnerId
      - feeAcceptanceIndc
    properties:
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      datePurchased:
        example: '2024-02-23'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      expirationDate:
        example: '2024-02-23'
        type: string
        format: date
      amountToBePosted:
        example: 2
        type: number
        minimum: 1
        maximum: 99999999
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      changeRoData:
        $ref: '#/definitions/changeRoData'
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
  vehicle-license-fee-refund:
    example:
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      firstPartnerId: V15
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownershipCertIssueDate: '2024-01-01'
      fileCode: '1'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      wreckOrLossDate: '2024-02-23'
      feeAcceptanceIndc: 'N'
      ownerNameOnRecord: ER4
      make: ACUR
      transactionDate: '2024-01-01'
      vinHin: JH4DB7560SS004122
      lienholderNameOnRecord: 'Y'
    type: object
    required:
      - ownerInfo
      - firstPartnerId
      - ownerAddress
      - secondPartnerId
      - wreckOrLossDate
      - feeAcceptanceIndc
      - ownerNameOnRecord
      - vinHin
    properties:
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/lienHolderNames'
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      wreckOrLossDate:
        example: '2024-02-23'
        type: string
        format: date
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      tnDate:
        example: '2024-10-01'
        type: string
        format: date
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
  miscellaneous-originals:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      asteriskYear: 2024
      bodyTypeModel: SU
      clearingIndc: 'N'
      dateFeesDue: '2024-01-01'
      dateFeesReceived: '2024-01-01'
      dealerDismantlerNumber: 1
      engineNum: 1DR4
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '2'
      firstPartnerId: V15
      fuelType: S
      inventoryCode:
        - '012'
      lawEnforcement: '00'
      make: ACUR
      modelYr: 2024
      numAxles: 4
      odometer: 2
      odometerCode: '68'
      odometerUnit: K
      priorHistoryIndc: T
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      unladenWgt: 2343
      vinHin: JH4DB7560SS004122
      yearFirstSold: 2023
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      lesseeAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      lienholderName:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      certificationDate: '2024-02-23'
      certificationIndc: C
      fhvutCode: F
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      inspSmog: 'Y'
      lesseeAddressIndc: 'Y'
      metalTab: 'Y'
      newPlateNumber: ER435TR
      organizationSymbol: V00
      outOfStateServiceFee: 'Y'
      planNonOper: C
      plateWithOwnerAssign: 'Y'
      plateWithOwnerFileCode: L
      plateWithOwnerLicense: 7YU
      plateWithOwnerName: DSW3
      plateWithOwnerReassign: 'Y'
      printTitle: 'Y'
      priorUseTax: 2344
      purchasePrice: 22.23
      remanufacturedVehicle: '3'
      reportOfSaleNum: 3E32WQE3
      rollback: '1'
      situsAddress: 123 MAIN STG
      situsCity: CA
      situsCountyCode: 23
      stickerNumber: '3E4'
      useTaxIndicator: 'Y'
      vlfWgtExempt: 'Y'
    type: object
    required:
      - bodyTypeModel
      - clearingIndc
      - dateFeesDue
      - feeAcceptanceIndc
      - firstPartnerId
      - fuelType
      - make
      - modelYr
      - secondPartnerId
      - typeLicenseCode
      - vinHin
      - yearFirstSold
      - ownerAddress
      - lienholderName
      - printTitle
      - purchasePrice
      - useTaxIndicator
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      asteriskYear:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      bodyTypeModel:
        example: SU
        type: string
        minLength: 2
        maxLength: 7
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesDue:
        example: '2024-01-01'
        type: string
        format: date
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      dealerDismantlerNumber:
        example: 1
        type: integer
        minimum: 1
        maximum: 99998
      engineNum:
        example: 1DR4
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      modelYr:
        example: 2024
        type: integer
        minimum: 1900
        maximum: 2050
      numAxles:
        example: 4
        type: integer
      odometer:
        example: 2
        type: integer
        minimum: 1
        maximum: 999999999
      odometerCode:
        $ref: '#/definitions/odometerCode'
      odometerUnit:
        $ref: '#/definitions/odometerUnit'
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      unladenWgt:
        example: 2343
        type: number
        minimum: 1
        maximum: 99999
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      yearFirstSold:
        example: 2023
        type: integer
        minimum: 1900
        maximum: 2050
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      ownerInfo:
        type: array
        items:
          $ref: '#/definitions/names'
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      inspSmog:
        $ref: '#/definitions/inspSmog'
      lesseeAddressIndc:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      metalTab:
        $ref: '#/definitions/metalTab'
      newPlateNumber:
        example: ER435TR
        type: string
        minLength: 7
        maxLength: 8
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      outOfStateServiceFee:
        $ref: '#/definitions/outOfStateServiceFee'
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        example: 7YU
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        example: DSW3
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      printTitle:
        $ref: '#/definitions/printTitle'
      priorUseTax:
        example: 2344
        type: number
        minimum: 1
        maximum: 99999
      purchasePrice:
        example: 22.23
        type: number
        minimum: 1
        maximum: 9999999
      remanufacturedVehicle:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      reportOfSaleNum:
        example: 3E32WQE3
        type: string
        minLength: 8
        maxLength: 8
      rollback:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      situsAddress:
        example: 123 MAIN STG
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 23
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: '3E4'
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      useTaxIndicator:
        $ref: '#/definitions/useTaxIndicator'
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
  legal-owner-transfer:
    example:
      accountNumber: qwe
      allocatedCounty: '19'
      certificationDate: '2024-02-23'
      certificationIndc: C
      clearingIndc: 'N'
      dealerDismantlerNumber: 1
      equipNum: '12'
      feeAcceptanceIndc: 'N'
      fileCode: '1'
      firstPartnerId: V15
      grossCombinedWeight: '2'
      grossVehicleWeight: '3'
      lienholderNameOnRecord: 'Y'
      lienholderName:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
      make: ACUR
      priorUseTax: 23
      planNonOper: C
      rdfCode:
        - '2'
      rdfIndicator: 'Y'
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      typeLicenseCode: '11'
      vinHin: JH4DB7560SS004122
      vlfWgtExempt: 'Y'
      certNonOperationDate: '2024-02-23'
      certNonOperationIndc: S
      costValue: 2
      lastTransferDate: '2024-02-23'
      lengthInches: 22
      musselFee: 'Y'
      numOfTransfers: 2
      ownerNameOnRecord: ER4
      ownershipCertIssueDate: '2024-01-01'
      priorPlateWithOwnerDisp: L
      repossessionDate: '2024-01-01'
      transCode: 'N'
      tnDate: '2024-01-01'
      fuelType: S
      dateFeesReceived: '2024-01-01'
      expirationDate: '2024-01-01'
      newPlateNumber: ER43DE3
      printTitle: 'Y'
      ownerAddress:
        street1: 6399 Morningstar Dr
        street2: '001'
        street3: SDS
        city: The Colony
        state: TX
        zip: '75056'
        county: 22
      ownerInfo:
        - nameTxt: SAM
          typeIndc: '2'
          codeDlnCurr: 22R453FR
    type: object
    required:
      - expirationDate
      - feeAcceptanceIndc
      - firstPartnerId
      - lienholderName
      - ownerNameOnRecord
      - printTitle
      - regPlateNumber
      - secondPartnerId
      - vinHin
      - ownerAddress
    properties:
      accountNumber:
        example: qwe
        type: string
        minLength: 1
        maxLength: 4
      allocatedCounty:
        example: '19'
        type: string
        minLength: 2
        maxLength: 2
      certificationDate:
        example: '2024-02-23'
        type: string
        format: date
      certificationIndc:
        $ref: '#/definitions/certificationIndc'
      certNonOperationDate:
        example: '2024-02-23'
        type: string
        format: date
      certNonOperationIndc:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      clearingIndc:
        $ref: '#/definitions/clearingIndc'
      dateFeesReceived:
        example: '2024-01-01'
        type: string
        format: date
      dupOwnershipCert:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      equipNum:
        example: '12'
        type: string
        minLength: 1
        maxLength: 7
      expirationDate:
        example: '2024-02-23'
        type: string
        format: date
      feeAcceptanceIndc:
        $ref: '#/definitions/feeAcceptanceIndc'
      fileCode:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      grossCombinedWeight:
        example: '2'
        type: string
        minLength: 1
        maxLength: 1
      grossVehicleWeight:
        example: '3'
        type: string
        minLength: 1
        maxLength: 1
      insuranceIndicator:
        $ref: '#/definitions/insuranceIndicator'
      inventoryCode:
        type: array
        maxItems: 2
        items:
          $ref: '#/definitions/inventoryCode'
      inspSmog:
        $ref: '#/definitions/inspSmog'
      lawEnforcement:
        $ref: '#/definitions/lawEnforcement'
      lengthInches:
        example: 22
        type: number
        minimum: 0
        maximum: 99
      lesseeAddressIndc:
        example: D
        type: string
        minLength: 1
        maxLength: 1
      lesseeChangeOnlyIndc:
        $ref: '#/definitions/lesseeChangeOnlyIndc'
      lienholderName:
        type: array
        maxItems: 3
        items:
          $ref: '#/definitions/lienHolderNames'
      make:
        example: ACUR
        type: string
        minLength: 2
        maxLength: 5
      metalTab:
        $ref: '#/definitions/metalTab'
      musselFee:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      newPlateNumber:
        example: R43E345R
        type: string
        minLength: 7
        maxLength: 8
      organizationSymbol:
        $ref: '#/definitions/organizationSymbol'
      ownerNameOnRecord:
        example: ER4
        type: string
        minLength: 1
        maxLength: 27
      ownershipCertIssueDate:
        example: '2024-01-01'
        type: string
        format: date
      priorHistoryIndc:
        $ref: '#/definitions/priorHistoryIndc'
      priorPlateWithOwnerDisp:
        $ref: '#/definitions/priorPlateWithOwnerDisp'
      planNonOper:
        $ref: '#/definitions/planNonOper'
      plateWithOwnerAssign:
        $ref: '#/definitions/plateWithOwnerAssign'
      plateWithOwnerFileCode:
        $ref: '#/definitions/plateWithOwnerFileCode'
      plateWithOwnerLicense:
        example: 43E
        type: string
        minLength: 2
        maxLength: 7
      plateWithOwnerName:
        example: SAM
        type: string
        minLength: 1
        maxLength: 27
      plateWithOwnerReassign:
        $ref: '#/definitions/plateWithOwnerReassign'
      printTitle:
        $ref: '#/definitions/printTitle'
      rdfCode:
        type: array
        maxItems: 8
        items:
          $ref: '#/definitions/rdfCode'
      rdfIndicator:
        $ref: '#/definitions/rdfIndicator'
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      situsAddress:
        example: 123 MAIN ST
        type: string
        minLength: 1
        maxLength: 47
      situsCity:
        example: CA
        type: string
        minLength: 2
        maxLength: 13
      situsCountyCode:
        example: 12
        type: integer
        minimum: 0
        maximum: 99
      stickerNumber:
        example: 123E
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 8
      substitutePlate:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      substituteSticker:
        example: '1'
        type: string
        minLength: 1
        maxLength: 1
      typeLicenseCode:
        example: '11'
        type: string
        minLength: 2
        maxLength: 2
      vinHin:
        example: JH4DB7560SS004122
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
      vlfWgtExempt:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 1
      lesseeAddress:
        $ref: '#/definitions/address'
      lienholderAddress:
        $ref: '#/definitions/address'
      ownerAddress:
        $ref: '#/definitions/ownerAddress'
      arbProof:
        $ref: '#/definitions/arbProof'
      fhvutCode:
        $ref: '#/definitions/fhvutCode'
      fuelType:
        example: S
        type: string
        minLength: 1
        maxLength: 1
      lienholderNameOnRecord:
        example: 'Y'
        type: string
        minLength: 1
        maxLength: 27
  retrieve-prior-transaction:
    example:
      firstPartnerId: V15
      regPlateNumber: 2VUB901
      secondPartnerId: BM
      transactionDate: '2024-02-23'
      vin: JNKAY01FX75YH2YTY
    type: object
    required:
      - firstPartnerId
      - secondPartnerId
    properties:
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      regPlateNumber:
        example: 2VUB901
        type: string
        minLength: 6
        maxLength: 8
      secondPartnerId:
        example: BM
        type: string
        minLength: 2
        maxLength: 2
      transactionDate:
        type: string
        format: date
      transactionId:
        type: string
      vin:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 30
  retrieve-fee-summary:
    example:
      firstPartnerId: V15
      finBusinessDate: '2024-01-23'
    type: object
    required:
      - firstPartnerId
      - finBusinessDate
    properties:
      firstPartnerId:
        example: V15
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      finBusinessDate:
        example: '2024-01-23'
        type: string
        format: date
  verifyInventory:
    example:
      firstPartnerId: V04
      invActDate: '2024-08-18'
      invAction: E
      invBegRange: '111'
      invEndRange: '9999999999'
      invItemCode: V
      invRangeQt: 999999
      invSendDate: '2024-08-17'
      secondPartnerId: AQ
    type: object
    required:
      - firstPartnerId
      - invActDate
      - invAction
      - invBegRange
      - invEndRange
      - invItemCode
      - invRangeQt
      - invSendDate
      - secondPartnerId
    properties:
      firstPartnerId:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 3
        maxLength: 3
      invActDate:
        type: string
        format: date
      invAction:
        type: string
        minLength: 1
        maxLength: 6
      invBegRange:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 10
      invEndRange:
        type: string
        pattern: ^[a-zA-Z0-9]*$
        minLength: 1
        maxLength: 10
      invItemCode:
        type: string
        minLength: 1
        maxLength: 3
      invRangeQt:
        type: integer
        minimum: 1
        maximum: 999999
      invSendDate:
        type: string
        format: date
      secondPartnerId:
        type: string
        minLength: 2
        maxLength: 2
  verifyInventorySample:
    example:
      transactionId: abcdef
      message: Success
      errorDetails:
        - code: ''
          text: ''
    type: object
    required:
      - errorDetails
    properties:
      transactionId:
        x-amf-union:
          - type: string
          - type: 'null'
      message:
        x-amf-union:
          - type: string
          - type: 'null'
      errorDetails:
        type: array
        items:
          type: object
          properties:
            code:
              x-amf-union:
                - type: string
                - type: 'null'
            text:
              x-amf-union:
                - type: string
                - type: 'null'
  clearingIndc:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  feeAcceptanceIndc:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  rdfIndicator:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  nonRepairableReasonCode:
    enum:
      - B
      - O
      - S
    example: B
    type: string
    minLength: 1
    maxLength: 1
  lawEnforcement:
    enum:
      - '00'
      - '10'
    example: '00'
    type: string
    minLength: 2
    maxLength: 2
  priorPlateWithOwnerDisp:
    enum:
      - L
      - R
      - S
    example: L
    type: string
    minLength: 1
    maxLength: 1
  priorHistoryIndc:
    enum:
      - A
      - P
      - T
    example: T
    type: string
    minLength: 1
    maxLength: 1
  odometerCode:
    enum:
      - '68'
      - '69'
      - '72'
    example: '68'
    type: string
    minLength: 2
    maxLength: 2
  odometerUnit:
    enum:
      - K
      - M
    example: K
    type: string
    minLength: 1
    maxLength: 1
  transCode:
    enum:
      - B
      - C
      - D
      - F
      - J
      - K
      - L
      - 'N'
      - P
      - R
      - S
      - T
    example: S
    type: string
    minLength: 1
    maxLength: 1
  ownerAddress:
    type: object
    required:
      - street1
      - city
    properties:
      street1:
        $ref: '#/definitions/street1'
      street2:
        $ref: '#/definitions/street2'
      street3:
        $ref: '#/definitions/street2'
      city:
        $ref: '#/definitions/city'
      state:
        $ref: '#/definitions/state'
      zip:
        $ref: '#/definitions/zip'
      county:
        $ref: '#/definitions/county'
  inventoryCode:
    example: '012'
    type: string
    pattern: ^[a-zA-Z0-9]*$
    minLength: 3
    maxLength: 3
  rdfCode:
    example: '2'
    type: string
    minLength: 1
    maxLength: 1
  names:
    type: object
    required:
      - nameTxt
      - typeIndc
    properties:
      nameTxt:
        $ref: '#/definitions/nameTxt'
      typeIndc:
        $ref: '#/definitions/typeIndc'
      codeDlnCurr:
        $ref: '#/definitions/codeDlnCurr'
  certificationIndc:
    enum:
      - C
      - D
      - U
    example: C
    type: string
    minLength: 1
    maxLength: 1
  fhvutCode:
    enum:
      - F
      - C
      - R
    example: F
    type: string
    minLength: 1
    maxLength: 1
  inspSmog:
    enum:
      - B
      - 'N'
      - R
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  metalTab:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  organizationSymbol:
    enum:
      - '001'
      - 1$
      - 1+
      - 1#
      - 1&
      - V00
      - W06
    example: V00
    type: string
    minLength: 2
    maxLength: 3
  planNonOper:
    enum:
      - C
      - D
      - H
      - I
      - P
      - R
      - S
      - 'Y'
    example: C
    type: string
    minLength: 1
    maxLength: 1
  plateWithOwnerAssign:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  plateWithOwnerFileCode:
    enum:
      - A
      - C
      - L
      - M
      - S
      - T
    example: L
    type: string
    minLength: 1
    maxLength: 1
  plateWithOwnerReassign:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  arbProof:
    enum:
      - A
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  insuranceVerification:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  address:
    type: object
    properties:
      street1:
        $ref: '#/definitions/street1'
      street2:
        $ref: '#/definitions/street2'
      street3:
        $ref: '#/definitions/street2'
      city:
        $ref: '#/definitions/city'
      state:
        $ref: '#/definitions/state'
      zip:
        $ref: '#/definitions/zip'
      county:
        $ref: '#/definitions/county'
  printTitle:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  lienHolderNames:
    type: object
    required:
      - nameTxt
    properties:
      nameTxt:
        $ref: '#/definitions/nameTxt'
      typeIndc:
        $ref: '#/definitions/typeIndc'
      codeDlnCurr:
        $ref: '#/definitions/codeDlnCurr'
  jnkTransCode:
    enum:
      - J
      - R
    example: R
    type: string
    minLength: 1
    maxLength: 1
  retainPlateWithOwner:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  inspect:
    enum:
      - C
      - D
    example: C
    type: string
    minLength: 1
    maxLength: 1
  lesseeChangeOnlyIndc:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  useTaxReclassIndc:
    enum:
      - D
      - F
      - G
      - L
      - R
      - U
      - X
      - 'Y'
    example: D
    type: string
    minLength: 1
    maxLength: 1
  outOfStateTitleSurrender:
    enum:
      - 'N'
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  useTaxIndicator:
    enum:
      - E
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  hullMaterial:
    enum:
      - A
      - C
      - P
      - S
      - W
      - X
    example: A
    type: string
    minLength: 1
    maxLength: 1
  propulsion:
    enum:
      - A
      - H
      - I
      - J
      - 'N'
      - O
      - S
      - X
    example: A
    type: string
    minLength: 1
    maxLength: 1
  vesselType:
    enum:
      - M
      - H
      - I
      - E
      - J
      - 'N'
      - P
      - U
      - O
      - S
      - Q
      - X
    example: Q
    type: string
    minLength: 1
    maxLength: 1
  junkSalvage:
    enum:
      - J
      - S
    example: S
    type: string
    minLength: 1
    maxLength: 1
  outOfStateServiceFee:
    enum:
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  insuranceIndicator:
    enum:
      - 'N'
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  issueCaOwnershipCert:
    enum:
      - 'N'
      - 'Y'
    example: 'Y'
    type: string
    minLength: 1
    maxLength: 1
  changeRoData:
    enum:
      - 'N'
      - 'Y'
    example: 'N'
    type: string
    minLength: 1
    maxLength: 1
  street1:
    example: 6399 Morningstar Dr
    type: string
    minLength: 1
    maxLength: 27
  street2:
    x-amf-examples:
      example_0: '001'
      example_1: SDS
    type: string
    minLength: 1
    maxLength: 27
  city:
    example: The Colony
    type: string
    minLength: 1
    maxLength: 27
  state:
    example: TX
    type: string
    minLength: 2
    maxLength: 13
  zip:
    example: '75056'
    type: string
    minLength: 5
    maxLength: 5
  county:
    example: 22
    type: integer
    minimum: 0
    maximum: 99
  nameTxt:
    example: SAM
    type: string
    minLength: 1
    maxLength: 27
  typeIndc:
    enum:
      - '1'
      - '2'
      - '3'
    example: '2'
    type: string
    minLength: 1
    maxLength: 1
  codeDlnCurr:
    example: 22R453FR
    type: string
    minLength: 8
    maxLength: 8
securityDefinitions:
  securities-fragment.oauth_2_0_azuread_client_cred:
    type: oauth2
    flow:  application
    x-amf-describedBy:
      headers:
        Authorization:
          description: |
            Used to send a valid OAuth2 access token generated through AzureAD.
          type: string
      responses:
        '401':
          description: |
            Token has been revoked.
        '403':
          description: |
            Bad OAuth request (wrong client-id/secret, scopes etc).
    tokenUrl: https://api.dxp-test.dmv.ca.gov:443/gw/vr-authentication-eapi-v1/token
    scopes:
      .default: 'null'
    x-amf-settings:
      authorizationGrants:
        - client_credentials



Please read the [Code of Conduct](https://nextcloud.com/community/code-of-conduct/). This document offers some guidance to ensure Nextcloud participants can cooperate effectively in a positive and inspiring atmosphere and to explain how together we can strengthen and support each other.

Please review the [guidelines for contributing](.github/CONTRIBUTING.md) to this repository.

More information on how to contribute: [https://nextcloud.com/contribute/](https://nextcloud.com/contribute/)
