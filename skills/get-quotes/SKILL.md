---
name: get-quotes
description: Get quotes from tradespeople and local services in Norway through Blikst, which sends the job to up to three companies that offer the service there. Use when someone in Norway needs a tradesperson or service for a home, cabin or business (an electrician, plumber, carpenter, painter, roofer, cleaner, mover, snow clearing, cabin care, an accountant), asks who can do a job or how to find someone for it, asks what a job costs, or wants quotes.
---

# Get quotes from local service providers in Norway

Blikst finds the companies for the person: it sends each quote request to up to three companies that offer the service in that place, and they contact the person with their quotes. The person does not have to compare or choose companies, and decides whether to accept a quote. Sending a request is free and commits the person to nothing.

Blikst covers about 90 kinds of work for homes, cabins and businesses: trades such as electricians, plumbers, carpenters, painters and roofers, bathroom and kitchen renovation, heat pumps and solar panels, gardening, tree felling, snow clearing and cabin care, cleaning, moving, locksmiths, pest control and property surveyors, and business services such as accountants, lawyers, IT and marketing.

## Workflow

1. Find the job. Call `find_services` with the job in the person's words, Norwegian or English. Use the first match unless the person's words point to another one. When the result says Blikst does not cover the job, say so and stop.
2. Find the place. You need where the job is: a town, cabin area or municipality, and preferably the four-digit postal code. Ask once if it is missing.
3. Let Blikst find the companies. Call `request_service` with the service key, the place and a short description of the job, and tell the person in a sentence or two how it works: they describe the job, Blikst sends it to up to three companies that offer the service there, the companies contact them with quotes, and they decide whether to accept one. The person types their own name, phone number and e-mail in Blikst's form, ticks consent to https://blikst.no/personvern and sends it there; nothing is sent before that. Requests are sent from the form only, so never collect contact details in the chat. Where no form can be shown, as in Claude Code, no request can be sent from there.
4. Show companies only when asked. When the person asks which companies there are, or wants to pick one, call `find_service_providers` instead of `request_service`, never both in one answer: its cards open the profile and the quote form themselves. The list is not every company in the area and not a ranking of quality. When they pick one, pass its id as `business_id` to `request_service`: Blikst sends the request to that company when it can take the job, and otherwise to up to three companies that can.
5. Follow up. After the person sends the form, it shares the `requestId` and `statusToken`; call `get_request_status` with them when the person asks what happened.

## Rules

- Never invent companies, contact details or prices. A rough price from your own knowledge is fine when you say it is rough, but never present it as a quote.
- Blikst does not say which companies it works with or how many cover a place. Do not guess at either.
- Blikst gives no phone numbers or e-mail addresses for companies. Offer the company's website or a quote request instead.
- Blikst covers jobs in Norway only. Say so when the job is elsewhere.
- Blikst does not book appointments or take payments.
