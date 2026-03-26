# Newsletter Draft: Data Viz Tools in 2026

Data visualization has come a long way since the days of Excel charts. Today's tools offer unprecedented flexibility and power.

> [!comment]- [question] **@chekos** · 2026-03-20 · re: "unprecedented flexibility and power"
> Is this too hyperbolic? Should we tone it down or back it up with specifics?
>> [!comment] **@claude** · 2026-03-25
>> It does read a bit hyperbolic without support. You could either tone it down to something like "remarkable flexibility" or anchor it with a concrete example — e.g., "from GPU-accelerated rendering to grammar-of-graphics APIs, today's tools offer flexibility that would have been hard to imagine a decade ago." That way the claim earns its weight.

## The Python Ecosystem

Python remains the dominant language for data visualization. Libraries like Matplotlib, Seaborn, and Plotly cover everything from publication-quality static charts to interactive dashboards.

The newcomer to watch is PyGWalker, which brings a Tableau-like interface directly into Jupyter notebooks. It's gained 15,000 GitHub stars in just six months.

> [!comment]- [flag] **@chekos** · 2026-03-20 · re: "15,000 GitHub stars in just six months"
> Need to verify this number — it might be outdated by now. Check the actual repo.
>> [!comment] **@claude** · 2026-03-25
>> I can't verify the current star count directly, but given this was written in March 2026 and the number may have been accurate at some earlier point, it's likely stale by now. I'd suggest replacing the specific number with a freshly checked figure, or using vaguer but safer language like "rapidly gaining popularity on GitHub." This is one to verify before publishing — check https://github.com/Kanaries/pygwalker for the latest count.

## Observable and the JavaScript Renaissance

Observable Plot has quietly become one of the best charting libraries available. Its concise API and sensible defaults make it a joy to use.

> [!comment]- **@chekos** · 2026-03-20 · re: "Observable Plot"
> I should probably mention D3 here too since Observable is built on it. But I don't want to get into a whole D3 tutorial tangent.
>> [!comment] **@claude** · 2026-03-25
>> A single sentence acknowledging the lineage is enough — something like "Built on top of D3, Observable Plot trades raw power for ergonomics, giving you sensible defaults without needing to write bindable joins." That credits D3 without opening the tutorial tangent. You could even link to D3 for curious readers and move on.

## The No-Code Movement

Tools like Datawrapper and Flourish have made it possible for journalists and non-programmers to create publication-quality visualizations. The Washington Post and The New York Times both use these tools regularly.

## What I'm Excited About

Personally, I think the most exciting development is the convergence of AI and data viz. Tools that can automatically suggest the best chart type for your data, or generate natural language descriptions of trends, are going to change how we communicate with data.
