# Lab Architecture

## Objective
Design and deploy an Elastic Stack-based SOC Detection Engineering lab simulating enterprise endpoint monitoring.

## Components
- Ubuntu Server (Elasticsearch, Kibana, Fleet)
- Windows 10 Endpoint (Elastic Agent, Elastic Defend)

## Telemetry Flow
Windows Endpoint → Elastic Agent → Fleet → Elasticsearch → Kibana

## Engineering Goal
Establish reliable telemetry ingestion before detection development.
