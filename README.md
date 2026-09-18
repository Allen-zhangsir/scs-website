# SCS Website

Official website repository for **Yangzhou Suchangshu Information Technology Co., Ltd. (扬州市素常数信息技术有限公司)**.

Primary production domain: `https://suchangshu.com`

This repository stores the versioned website source and deployment artifacts for the SCS official website.

## Deployment target

- Tencent Cloud SCF
- Region: `ap-guangzhou`
- Namespace: `default`
- Function: `scs-website`
- Runtime: `Nodejs18.15`
- Handler: `index.main_handler`

## Current baseline

Website baseline: V1.1 bilingual, mainland-access-oriented deployment candidate.

Chinese: `/`
English: `/en/`

No secrets, cloud credentials, OAuth tokens, or private keys are stored in this repository.
