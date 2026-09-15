# Portfolio Tracker MVP Requirements

## Product goal

Enable an individual investor to securely record investment activity, see the current value and performance of their portfolio, and understand how it is allocated. Financial figures are calculated by the application; no AI analysis is included in this MVP.

## Scope assumptions

- The MVP supports one portfolio per registered user and only the portfolio owner may view or change its data.
- The first release supports equities, ETFs, bonds, treasury bills, commercial paper, mutual funds, infrastructure funds, cash, and cryptocurrency as asset types.
- An asset has one reporting currency. Multi-currency conversion and live market-data integrations are out of scope; users enter the current price manually.
- Buy and sell transactions use weighted-average cost basis. Transaction fees are included in the purchase cost basis and deducted from sale proceeds.
- A sale cannot exceed the quantity currently held. Short positions are out of scope.
- Deposits and withdrawals affect cash/invested amounts but are not gains, losses, or income.
- Dividends and interest are recorded as income and do not change a holding's quantity or cost basis.
- Asset prices and transactions are entered manually. Importing data, recurring transactions, tax reporting, alerts, benchmarks, charts, and the AI Portfolio Analyst are post-MVP work.

## Features

### F1. Account access and profile

Users can register, sign in, sign out, and view basic profile information. Access to portfolio data requires authentication.

### F2. Asset catalogue

Users can create and manage the investment assets used in their portfolio. An asset records its name, symbol/ticker, type, currency, market, and optional sector/category.

### F3. Transaction recording

Users can record dated buys, sells, dividends, interest, fees, deposits, and withdrawals. Each transaction preserves the values entered at the time of recording and may be corrected or removed by its owner.

### F4. Holdings and deterministic performance

The application derives holdings from transactions and current prices. It shows quantity, average cost, cost basis, current value, realized gain/loss, unrealized gain/loss, and income received using defined calculation rules.

### F5. Portfolio dashboard and allocation

The dashboard summarizes portfolio value, invested amount, gain/loss, return percentage, income, allocation, and recent activity. Users can review a full transaction history.

## User stories and acceptance criteria

### US1. Register and authenticate

As an investor, I want to create an account and sign in, so that my portfolio is private.

Acceptance criteria:

- A user can register with a valid, unique email address and password.
- A registered user can sign in with valid credentials and sign out.
- Invalid credentials or a duplicate registration are rejected without exposing whether an account exists beyond the appropriate validation message.
- Unauthenticated users cannot access portfolio, asset, transaction, holdings, or dashboard data.
- A signed-in user can view their basic profile information.

### US2. Manage my assets

As an investor, I want to maintain the assets I invest in, so that I can record transactions against them.

Acceptance criteria:

- A user can create an asset with name, asset type, and currency; symbol/ticker, market, and sector/category are optional.
- The asset type must be one of the MVP-supported types.
- A user can view and edit only their own assets.
- An asset cannot be deleted while it has transactions; the user receives a clear explanation.
- An asset's current price can be entered or updated manually, and its price date is retained.

### US3. Record investment and cash activity

As an investor, I want to record portfolio transactions, so that my holdings and portfolio results are accurate.

Acceptance criteria:

- A user can create a dated buy or sell with an asset, quantity, unit price, and optional fee.
- A buy requires a quantity and unit price greater than zero; a sell cannot make the holding quantity negative.
- A user can create a dated dividend or interest transaction with an amount greater than zero.
- A user can create a dated fee, deposit, or withdrawal transaction with an amount greater than zero.
- A transaction is visible only to its owner and is included in that owner's calculations.
- The user can edit or delete their transaction; holdings and dashboard figures recalculate from the saved transaction history.
- Invalid or incomplete transaction data is rejected with a clear validation message and does not change portfolio calculations.

### US4. View holdings and performance

As an investor, I want to see each current holding and its performance, so that I can understand my investment position.

Acceptance criteria:

- Holdings are derived from transactions and display only assets with a positive quantity.
- Each holding displays quantity, average cost per unit, cost basis, latest current price, current value, unrealized gain/loss, realized gain/loss, and income received.
- For a buy, cost basis increases by `quantity × unit price + fee`; average cost is the resulting cost basis divided by quantity held.
- For a sell, realized gain/loss equals `sale proceeds after fee − cost of units sold`, using the weighted-average cost immediately before the sale; remaining cost basis decreases by the cost of units sold.
- Unrealized gain/loss equals current value minus remaining cost basis. Current value equals quantity held multiplied by the latest entered current price.
- Dividend and interest amounts appear as income separately from capital gain/loss.
- If a holding has no current price, its value-dependent metrics are clearly unavailable rather than estimated or fabricated.

### US5. View the portfolio dashboard and allocation

As an investor, I want a concise portfolio summary, so that I can assess my overall position quickly.

Acceptance criteria:

- The dashboard displays total portfolio value, total invested amount, total gain/loss, return percentage, and total income received.
- Total gain/loss equals realized gain/loss plus unrealized gain/loss; income is displayed separately.
- Return percentage is calculated from gain/loss divided by total invested amount. If total invested amount is zero, the dashboard displays return as unavailable.
- Total invested amount reflects deposits less withdrawals and is not altered by buy, sell, dividend, interest, or fee transactions.
- Allocation is available by asset type and by individual holding. Each allocation percentage uses current holding value divided by total portfolio value.
- The dashboard shows recent transactions in reverse chronological order.
- A transaction-history view lists all of the user's transactions with date, type, related asset where applicable, amount details, and fee where applicable.

### US6. Keep user data isolated

As an investor, I want my portfolio kept separate from other users' portfolios, so that my financial information remains private.

Acceptance criteria:

- A user cannot retrieve, modify, or delete another user's profile, assets, transactions, holdings, dashboard, or history through the user interface or API.
- Portfolio calculations use only the authenticated user's assets and transactions.
- Authentication secrets, passwords, and access tokens are never displayed in the application or included in normal responses.

## MVP exclusions

- AI-generated portfolio analysis or investment advice
- Live prices, automatic price refresh, or brokerage/market-data integrations
- Foreign-exchange conversion and consolidated multi-currency reporting
- Multiple portfolios, shared portfolios, or adviser access
- CSV imports/exports, recurring investments, alerts, tax reports, benchmarks, and performance charts
- Trade execution or any autonomous investment action

## Definition of done for an MVP feature

A feature is ready for release when its acceptance criteria pass, deterministic calculation cases are covered by automated tests where applicable, authorization behavior is verified, and QA independently validates it against this document.
