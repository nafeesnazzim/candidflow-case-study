# Candidflow – Secure Recruitment Tracker on AWS (Case Study)

A write-up of my role on a university team project. The application's source code belongs to the team's repository and is not included here.

## Overview
Candidflow is a role-based recruitment tracker (Django, PostgreSQL) deployed live on AWS, built by a four-person university team between July and September 2026.

**Live demo (team deployment):** https://dmy7zm623g8ab.cloudfront.net/

## My role: Scrum Master
- Facilitated 38 meetings (stand-ups, planning sessions and reviews) across two sprints.
- Owned cost and infrastructure risks in the project's 32-item risk register.

## AWS work I did
- Configured IAM users, roles and policies.
- Configured Elastic Beanstalk, EC2 and Amazon RDS (PostgreSQL) for production.
- Replaced a $50 budget alert with a zero-spend alert, so that any spend on the credit-funded account raises an alert straight away.

## Security design I contributed to
- Role-based access control across eight roles
- Audit logging
- Validated file uploads
- Advisory-only CV screening aligned with UK GDPR: the system suggests, a person decides

## Incidents I diagnosed and fixed
**1. Missing database connection setting**
- What happened: the production application could not reach its database because a required connection setting was missing from its configuration.
- Root cause: the configuration was judged by whether the app appeared to work, not checked against its intended state.
- Preventive control: check every required setting against a documented list of the intended configuration before each deployment.

**2. EC2 instance profile attached directly to the instance**
- What happened: the instance profile had been attached to the EC2 instance by hand, outside Elastic Beanstalk's own environment configuration.
- Root cause and risk: Elastic Beanstalk manages its instances, so a manual change on one instance is not part of the managed configuration and can be lost when the instance is replaced.
- Preventive control: make infrastructure changes only through the Elastic Beanstalk environment configuration.

## What I learned
I had been verifying configuration by whether things appeared to work, instead of checking it against its intended state. In cloud security that gap matters: misconfiguration is consistently ranked among the top cloud threats (for example by the Cloud Security Alliance), and a setup that "works" can still be wrong in ways that only show up as an outage or an exposure.
