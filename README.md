# Microsoft 365 templates and snippets

Free, copy-ready snippets I use on real Microsoft 365 projects: Power Automate expressions, SharePoint OData filter queries, Exchange Online PowerShell, SharePoint column validation and planning checklists.

Each section links to a full, plain-English guide with screenshots, explanations and FAQs on [winstack365.com/guides](https://winstack365.com/guides).

Maintained by [Daniel Awokunle](https://winstack365.com/about), Microsoft 365 consultant at [Winstack365](https://winstack365.com).

---

## Power Automate: convert UTC to local time

Power Automate works in UTC. Convert before you show a time to people:

```
convertFromUtc(utcNow(), 'GMT Standard Time', 'dd MMM yyyy HH:mm')
```

Common time zone names: `Eastern Standard Time`, `Pacific Standard Time`, `GMT Standard Time` (UK), `AUS Eastern Standard Time`, `Arabian Standard Time` (UAE). The name is the Windows time zone ID, not the city.

Full guide: [Power Automate: Convert UTC to Local Time (convertFromUtc Examples)](https://winstack365.com/guides/power-automate-convert-utc-to-local-time)

## Power Automate: Excel date shows as a number (46340)

Excel stores dates as the number of days since 30 December 1899. Turn the number into a date:

```
formatDateTime(addDays('1899-12-30', int(items('Apply_to_each')?['Date'])), 'yyyy-MM-dd')
```

Or set **DateTime Format** to **ISO 8601** in the advanced options of *List rows present in a table*, and Excel dates arrive as real dates.

Full guide: [Excel Date Showing as a Number in Power Automate](https://winstack365.com/guides/power-automate-excel-date-showing-as-number)

## SharePoint OData filter queries (Get items)

Use the column's **internal name**, single quotes around text, and no quotes around numbers.

| Column type | Filter Query |
|---|---|
| Text | `Title eq 'Harbor and Pine'` |
| Choice | `Status eq 'Approved'` |
| Number | `Amount gt 500` |
| Yes/No | `IsActive eq 1` |
| Date | `DueDate le '2026-12-31'` |
| Person | `AssignedTo/EMail eq 'emma@example.com'` |
| Empty value | `Department eq null` |
| Combined | `Status eq 'Open' and Amount gt 500` |

Full guide: [Power Automate OData Filter Query Examples (SharePoint Get Items)](https://winstack365.com/guides/power-automate-odata-filter-query-examples)

## Exchange Online: keep sent items in the shared mailbox

By default, email sent from a shared mailbox is saved in the sender's own Sent Items. Turn on both copy settings so the team can see it:

```powershell
Connect-ExchangeOnline
Set-Mailbox -Identity info@example.com -MessageCopyForSentAsEnabled $true -MessageCopyForSendOnBehalfEnabled $true
```

Full guide: [Shared Mailbox Emails Saved in Your Sent Items: The Fix](https://winstack365.com/guides/shared-mailbox-sent-items-personal)

## SharePoint column validation: phone numbers that allow international formats

A rule that forces exactly 10 digits rejects valid UK, Australian and UAE numbers. Keep the column as **Single line of text** (so leading zeros and `+` are kept) and allow a sensible length:

```
=AND(LEN([Phone])>=8, LEN([Phone])<=16)
```

## Microsoft 365 after a merger: tenant-to-tenant checklist

1. Decide: connect the two tenants first (shared free/busy, guest access) or merge now.
2. Inventory: users, shared mailboxes, SharePoint sites and Teams with owners, domains and DNS, connected apps, retention and legal holds.
3. Clean up before you move, and map old folders to new libraries and owners.
4. Choose the route: Microsoft cross-tenant migration (add-on licence per user) or a third-party tool. Teams chats are the hard part.
5. Domain cutover in order: move mailboxes, remove the domain from the old tenant, add it to the new one, update DNS. Keep old addresses as aliases.
6. Day one note for staff: new sign-in and MFA, Outlook profile, OneDrive and Teams, where files live, who to call.
7. Keep the old tenant until you are sure nothing is missing.

Full guide and video: [Microsoft 365 After a Merger: Tenant-to-Tenant Migration Checklist](https://winstack365.com/guides/microsoft-365-tenant-to-tenant-migration-after-acquisition)

## More free tools

- [Copilot readiness self-check](https://winstack365.com/copilot-readiness-check): 12 questions, instant score and what to fix first
- [Microsoft 365 clean-up checklist](https://winstack365.com/free-checklist)
- [All guides](https://winstack365.com/guides)

---

Found a mistake or want a snippet added? Open an issue. Need it done for you? [Book a free 30-minute call](https://winstack365.com/contact).

Licence: MIT. Use these snippets freely.
