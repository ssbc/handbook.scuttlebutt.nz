# Feed

A feed is a signed append-only sequence of messages. Each identity has exactly one feed.

Note that append-only means you cannot delete an existing message, or change your history. This is enforced by a per-feed blockchain. This is to ensure the entire network converges on the same state.
