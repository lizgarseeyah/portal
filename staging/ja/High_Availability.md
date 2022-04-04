# High availability

日本語コンテンツ

---

# High availability

## Background

Business continuity and disaster recovery are an important
requirement for Best For You Organics' API. This can be
accomplished by a multi-region deployment in the cloud.

## Challenge

Your challenge is to deploy or extend your production Ratings
API and backend database to at least one more Azure region and
distribute the traffic between them having one as the primary
region and the other as the backup region.

Also discuss (or implement) with your team the changes and
considerations needed if you were to implement this on a
performance basis, with the solution deployed to multiple
regions and traffic routed based on performance.

Once you have your solution working, let your coach know. Once
you are validated you are now Serverless OpenHack masters!

Congratulations!!

## Success Criteria

* Demonstrate to your coach how you implemented the solution.
Your production Ratings API and database should both be running
in at least two Azure regions with one primary and the other
secondary in priority

* Provide your coach with the new entry URL for the Ratings API
that has been deployed to at least one more region. The coach
should be able to make the same calls to this new URL as from
Challenge 2

## References

* [Overview of Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)
* [Business continuity and disaster recovery (BCDR): Azure Paired Regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)
* [How to distribute data globally with Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/distribute-data-globally)

## Progress Diagram

 ![Final progress diagram](https://serverlessoh.azureedge.net/public/final-progress-diagram.jpg)
