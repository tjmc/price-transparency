# Stuff

[Source](https://github.com/CMSgov/price-transparency-guide)

`These machine-readable files must be made available to the public without restrictions that would impede the re-use of that information.`

I’d expect it be easier to find the URLs to the ToC but here’s my
working list

## Sites

### Blue Cross / Blue Shield of Illinois

[Website](https://www.bcbsil.com/member/policy-forms/machine-readable-file)

[Direct
link](https://app0004702110a5prdnc868.blob.core.windows.net/toc/2022-07-12_Blue-Cross-and-Blue-Shield-of-Illinois_index.json)

### ambetter

[ToC](https://api.centene.com/ambetter/reference/cms-data-index.json)

### Kaiser

[In-network](https://healthy.kaiserpermanente.org/pricing/innetwork/2022-07_List.txt)
[Out-of-network](https://healthy.kaiserpermanente.org/pricing/outofnetwork/2022-07_List.txt)

### Blue Shield of California

[List of
files](https://mrf.healthsparq.com/bsca-egress.nophi.kyruushsq.com/prd/mrf/BSCA_I/BSCA/latest_metadata.json)

## Issues

### Anthem Blue Cross

[ToC](https://antm-pt-prod-dataz-nogbd--us-east1.s3.amazonaws.com/anthem/2022-07-01_anthem_index.json.gz)

Looks like Anthem generated some entries using their HPI storage by
mistake. Try changing the hostname when you are processing the TOC.

     antm-pt-prod-dataz-nogbd-phi-us-east1.s3.amazonaws.com -> antm-pt-prod-dataz-nogbd-nophi-us-east1.s3.amazonaws.com

## Against the spirit

### UHC

Loads javascript site

#### Workaround

    Grab the blog list:

        https://uhc-sas-function-apim-prod.azure-api.net/api/blobs-function
        
        -----
        {
          "blobs": [
            {
              "name": "2022-07-01_02-GLOBAL-CHAUFFEURED-SERVICE_index.json",
              "origin": "uhc"
            },
            {
              "name": "2022-07-01_1-BETTER-LLC_index.json",
              "origin": "uhc"
            },
        ...
        

    Then use the filename to request the sasUrl from

        https://uhc-sas-function-apim-prod.azure-api.net/api/blob-sas?blobName=2022-07-01_02-GLOBAL-CHAUFFEURED-SERVICE_index.json
        -----
        {
          "sasUrl": "https://mrfstorageprod.blob.core.windows.net/mrf-even/2022-07-01_02-GLOBAL-CHAUFFEURED-SERVICE_index.json?blahblahblah"
        }
        

    Then use the sasUrl to download the file.

### Collective Health

No direct link to external sites. I’ll acknowlege Collective Health
probabably wasn’t able to get this info

https://transparency-in-coverage.collectivehealth.com/index.html

-   [In-network
    Rates](https://transparency-in-coverage.collectivehealth.com/in-network-rates-meta.txt)
-   [Out-network Allowed
    Amount](https://transparency-in-coverage.collectivehealth.com/allowed-amount-meta.txt)

<!-- -->

    Examples:

    File scope: In Network,Plan Name: In-Network,Sponsor EIN: 942606438,https://web.healthsparq.com/healthsparq/public/#/one/insurerCode=BSCA_I&brandCode=BSCA/machine-readable-transparency-in-coverage

    File scope: In Network,Plan Name: Kaiser,Sponsor EIN: 942606438,https://healthy.kaiserpermanente.org/pages/technical-information#machine-readable-files

    File scope: In Network,Plan Name: CDHP,Sponsor EIN: 593797948,https://www.anthem.com/ca/machine-readable-file/search

    File scope: In Network,Plan Name: Standard,Sponsor EIN: 134012728,https://www.empireblue.com/machine-readable-file/search

Broken link

    File scope: In Network,Plan Name: Base PPO,Sponsor EIN: 742149829,https://staging.bcbsil.com/asomrf?EIN=742149829

### Medical Mutual

Need to scrape HTML
[](https://www.medmutual.com/For-Employers/Employer-Resources/Machine-Readable-Files.aspx)

    lynx -dump -hiddenlinks=listonly "https://www.medmutual.com/For-Employers/Employer-Resources/Machine-Readable-Files.aspx" |grep json | tee list.json

### Molina Healthcare of Ohio

    https://www.molinamarketplace.com/marketplace/oh/en-us/About/compinfo/PricingTransparency.aspx

    Currently shows

    | Table of Contents | Coming Soon |

That said,
\[\](https://www.molinamarketplace.com/PricingTransparency/263574/OH/2022-07-01_Molina-Healthcare-of-Ohio_index.json
used to work. - \[ \] [July, 2021 downloads](molina/)
