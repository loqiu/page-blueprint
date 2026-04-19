# Page Mode Reference

Use this file to classify the target page before drafting the blueprint.
After classification, open the canonical design sources in `../../../shared/design/global/` and the one matching file in `../../../shared/design/page-modes/`. This file is a routing aid, not the final source of truth.

## Global Baseline

Regardless of page mode:

- prioritize task clarity over polish
- follow global tokens, spacing, typography, semantic colors, and accessibility rules
- cover loading, empty, error, disabled, and other relevant states
- avoid decorative structures that do not improve decision making

## Overview Dashboard

Choose this mode when the page is summary-first.

- primary tasks: scan, compare, review trends, drill down
- dominant surfaces: KPI cards, trend charts, summary modules
- layout rule: KPI and trend region first, detail table later
- avoid: table-first structure, giant decorative cards, equal-weight widgets

## Monitoring Dashboard

Choose this mode when the page is status-first and recency-sensitive.

- primary tasks: monitor, detect degradation, investigate urgent changes
- dominant surfaces: status strip, health cards, alerts, recent events
- layout rule: critical status and alerts above general analytics
- avoid: burying freshness, hiding incidents in tabs, treating stale data as a footnote

## Operations Dashboard

Choose this mode when the page is action-first and list-driven.

- primary tasks: scan rows, filter, sort, act on items, inspect without losing context
- dominant surfaces: toolbar, summary strip, table or list, detail-on-demand
- layout rule: table/list is the main working surface
- avoid: pushing the table below charts, replacing row comparison with loose cards

## Detail Page

Choose this mode when the page is one-object-first.

- primary tasks: identify the object, understand current status, review context, take the next action
- dominant surfaces: summary header, metadata block, primary sections, history, related records
- layout rule: identity and current status must appear before supporting evidence
- avoid: giant hero banners, noisy headers, overusing tabs for shallow grouping

## Browse / Discovery Page

Choose this mode when the page is browse-first.

- primary tasks: browse, narrow, compare lightly, open promising objects
- dominant surfaces: result list, result grid, object-first cards
- layout rule: filters and result surface first, supporting metadata later
- avoid: dashboard-style KPI chrome, equal-weight cards everywhere, burying result identity

## Settings / Admin Page

Choose this mode when the page is configuration-first.

- primary tasks: review current settings, edit safely, understand scope and consequences
- dominant surfaces: sectioned forms, policy groups, admin tables
- layout rule: scope and section grouping first, helper and history later
- avoid: dashboard aesthetics, decorative hero zones, destructive actions mixed with save actions

## Mixed Pages

If the page mixes patterns:

1. decide what the user must finish first
2. choose the mode that best serves that task
3. allow other modes only as supporting sections

Never describe a page as equally belonging to multiple dominant modes.
