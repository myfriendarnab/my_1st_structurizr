# Going, Going, Gone

This is one famous kata of the architectural katas published in the "Fundamentals of Software Architecture" book.

I decided to use this Kata to build its architecture artifacts using several code-like tools like PlantUML

In this, I will build an initial architecture template for the rest of Katas that I will try to build in the coming days.

## Executive Summary

### Description 
An auction company wants to take its auctions online to a nationwide scale. Customers choose the auction to participate in, wait until the auction begins, then bid as if they are there in the room with the auctioneer. 

### Users 

Scale up to hundreds of participants per auction, potentially up to thousands of participants, and as many simultaneous auctions as possible. 

## Requirements

- Auctions must be as real-time as possible.
- Bidders register with a credit card; the system automatically charges the card if the bidder wins.
- Participants must be tracked via a reputation index.
- Bidders can see a live video stream of the auction and all bids as they occur.
- Both online and live bids must be received in the order in which they are placed.

## Additional Context

- Auction company is expanding aggressively by merging with smaller competitors.
- Budget is not constrained. This is a strategic direction.
- Company just exited a lawsuit where it settled a suit alleging fraud.
