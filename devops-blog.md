# DevOps, Meet Real-Time User Experience

*Writing sample: product blog post · Rich Slogar · [Download PDF](devops-blog.pdf)*

> **About this sample:** This blog content was written to help introduce Conviva App features to DevOps teams. The content is intended for external audiences interested in learning more about Conviva products. I collaborated with the product architect and product manager to align with current functionality and adoption strategies. Content for the related use cases was also developed and included in the Conviva Learning Center to help transition users from prospects to early adopters. Images intentionally blurred.

---

## Summary

With Conviva for App, you

- Develop a deeper understanding of what parts of your app are positively or negatively impacting user experiences.
- Monitor app user flows and receive notifications of real-time root cause detection the moment an issue exceeds persistence and impacted-device thresholds.
- Easily create custom metrics and KPIs that represent your most critical customer success behaviors and touchpoints, such as purchase confirmation and time to login.

In comparison, current observability tools strive to make sense of only low-level operational performance but remain disconnected from actual user experience or engagement. Although Product Analytics tools do focus on the client-side user engagement and behavior, they are not real-time, not targeted to operations teams, and rely only on engagement, ignoring the other critical pieces: experience and performance.

Despite well-written application code and multiple layers of performance monitoring, the complexities of modern web technology stacks make the DevOps tasks of maintaining high levels of user experience KPIs across web and native device applications increasingly difficult. Spikes in client-side requests/responses, front-end presentation latency, and diversified back-end data processing commonly underlie user experience issues which may elude current observability and performance monitoring and detection. The result is additional user engagement uncertainty and disconnects between root cause analysis and actual user experiences.

Most observability and monitoring tools rely only on a bottom-up approach traversing logs, traces, and performance metrics in search of pinpointing the technology paths that may or may not connect with the impacted user experience touch points.

Enter Conviva: Conviva for App starts with actual user experience measurements and metrics that empower insightful real-time data alerting and drilldowns into the affecting application root-cause layers—enabling rapid issue isolation and root cause resolution of actual experience impacts.

| App Issues Impacting User Experience | Conviva Metrics | Conviva Root Cause Dimensions |
| --- | --- | --- |
| • Slow app startup<br>• Slow screen transition / page loading<br>• Slow remote API response times, impacting individual widget updates<br>• Application crashes<br>• Application not responsive | • App *&lt;Metric&gt;*<br>• Screen *&lt;Metric&gt;*<br>• Page *&lt;Metric&gt;*<br>• Network Response *&lt;Metric&gt;*<br>• App *&lt;Metric&gt;*<br>• Application *&lt;Metric&gt;* | • App Name<br>• App Version, Build Version<br>• Device OS, OS Version<br>• Device Manufacturer, Model<br>• Browser Name, Version<br>• Screen Name, Page Title, Page Hostname / Path / Query / URL<br>• Network Request Hostname / Path / Query / URL / Response Status Code |

## How Does Conviva Do It?

### Time-state Processing and Server-Side Sessionization

Conviva for App applies stateful processing across the tech stack and user experiences maintaining real-time observability of the events, requests, and state changes that occur during each application session, enabling intelligent computations across these data points within each active session. No need to wait for session end and latency-plagued historical data gathering. The combination of sessionization, extensive dimensional metadata, and real-time metrics enable enhanced user experience observations and technology stack correlations, so DevOps teams can focus on resolving actual experience-impacting issues in real-time. Without the limits of stateless processing that only maintain isolated instantaneous data values stored independent of other previous event/state changes, Conviva for App stateful processing activates real-time operational analysis, letting you know when user experiences flag application issues and act quickly to rectify engagement and revenue impact risks.

Furthermore, user timelines allow you to debug app issues based on the actual session events.

For example, quickly recognize and remedy real-time spikes in user login issues impacting user access, using the Total Login Time metric to isolate the source of access-blocking issues across a comparative performance analysis of internal and 3rd-party authentication agents request and response times.

### Hypercube Engine

Conviva for App displays metric time series and distributions for session selection based on metric performance, along with dimensional tables that enable real-time comparative analysis of complex drill-downs across the session dimensional entities, such as specific network request durations across multiple page URLs.

Session selection based on a network request duration spike and average page load times from 0 to 5 seconds.

![Session selection based on a network request duration spike (image intentionally blurred)](images/devops-blog-1.png)

Dimension drill-down by offending network request API to compare page URL performance.

![Dimension drill-down by network request API (image intentionally blurred)](images/devops-blog-2.png)

![Page URL performance comparison (image intentionally blurred)](images/devops-blog-3.png)

Designed from the ground up for advanced real-time time-state metric comparisons at scale, these combinatorics across dimensional entities enable pattern correlation in user experience impacts with the performance of application computations and services. Derived from auto-collected and custom metric performance and the related dimension values, the correlation possibilities scale to match the complexities of modern web technology stacks, for example, performing comparative analysis drill downs to isolate application sessions with *Login Times* that spiked only on specific device operating systems in a limited geographic area.

Furthermore, Conviva's real-time time-state pipeline and computations run at the scale of Internet audiences with high availability and cost efficiency, performing context-sensitive computation over continuously evolving session states at a fraction of the latency and cost of traditional SQL-based computations.

- **Real-Time** – Low latency from raw event ingest to actionable insights enabling actionability in seconds to minutes.
- **High Performance** – Fast, interactive multi-dimensional queries with high concurrency on real-time and historical data enabling quick analysis by many users simultaneously.
- **Fully Integrated** – Integrated platform from raw event ingest to actionable insights, including the UI, eliminating the need for customers to piece together multiple big data systems.
- **Internet Scale** – Able to handle millions of concurrent endpoints with high volume of measurements.
- **High Efficiency** – Low cost (as much as 10x lower) compared to other technologies.

### Flexible Custom Metrics

Conviva for App introduces a new layer between the Conviva sensor and Pulse that visualizes the data pulled into Conviva from your app for custom metric compilation. Specifically, Metric Builder options enable custom time-interval and conversion metrics so that you can analyze complex app flow scenarios, such as analyzing the delay between when users login to their account and the start of video playtime.

- **Time Interval Metric:** Measures the duration between two events, such as the duration between the login screen event and the login success event.
- **Conversion Metric:** Measures the count or conversion rates of events from one stage to another, such as the count of sessions with successful login after opening the login screen.

Custom metrics appear in metric widgets with time series and dimension data for deep-dive analysis. For example, the custom metric *Full Login Time* displays the duration of the login form/page loading, user credential entry, form submission, and subsequent next page loading. Without speedy completion of authentication, all impacting user activities are restricted—lower active users, lower concurrent streams for video apps, and lower purchase rates for market-place apps.

Create your own custom metrics for tracking interval and conversion-based event analysis.

### AI Algorithms and AI Alerting

Often complex application performance and user experience issues remain undetected; here too, Conviva for App has you covered. AI-based algorithms and AI-driven alerts automatically surface anomalous events and insights to identify the under-performing root cause group that crossed the established performance baseline with significant unique user impacts. This example shows an AI alert for Avg Network Request Duration with performance baseline (dashed blue line), highlighted deviation spike (solid blue line) and impacted unique devices (orange line) and alert start/peak/end markers.

![AI alert for average network request duration (image intentionally blurred)](images/devops-blog-4.png)

### Flexible Ingest

Extending to cover the complete measurement spectrum of every activity on any app, device, firmware, OS, and more, Conviva for App goes well beyond web and native applications to support the comprehensive data ingestion from multiple sources anywhere in the world via a library of extremely lightweight SDKs. With this wide range of metric computations, dimensional drilldowns, and experience-based analysis, you can now easily and efficiently keep a clear focus on the complex DevOps interactions between your user experiences and digital systems.
