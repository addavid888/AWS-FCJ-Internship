---
title: "Location Intelligence for Sustainable Transportation on AWS"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

*by Mahesh Geeniga, Lev Levine, and Nicolas Legros on 14 MAY 2025*

*By Mahesh Geeniga, Senior Partner Solutions Architect – AWS, Lev Levine, Principal Partner Development Manager – AWS, Nicolas Legros, Director Product Marketing – HERE Technologies*

Location intelligence, powered by real-time geospatial data, is revolutionizing transportation and logistics by enabling businesses to optimize routes, reduce fuel consumption, and minimize environmental impact while meeting the growing demands of a global economy.

HERE Technologies, in collaboration with AWS, delivers advanced location intelligence solutions, including smart routing, real-time traffic monitoring, and sophisticated last-mile delivery planning. These solutions help companies reduce emissions while optimizing their deliveries, fleet management, and overall performance.

In this blog, you will explore how HERE’s next-generation mapping solutions on Amazon Web Services (AWS) are helping businesses achieve their sustainability goals. These solutions demonstrate that companies can maintain operational efficiency while being environmentally responsible.

**Smart Route Optimization**

HERE Technologies, a location intelligence leader, relies on AWS Cloud infrastructure for its advanced routing and navigation solutions, such as the [HERE Fleet Optimization](https://aws.amazon.com/marketplace/seller-profile?id=cc033bc0-fe05-4d79-ba58-9a132b1fe9d3) solution. AWS services, including Amazon S3, Amazon EC2, and AWS Batch, enable HERE to process massive amounts of real-time and historical data, transforming it into advanced routing intelligence.

The [HERE Tour Planning API](https://aws.amazon.com/marketplace/pp/prodview-izb3zaa6bhepo) optimizes entire vehicle fleets by creating routes that save both time and money. By using AWS Graviton processors, [HERE improves the API’s performance](https://aws.amazon.com/solutions/case-studies/here-technologies-case-study/) while lowering customer costs. The API creates balanced routes while optimizing vehicle usage, incorporating various operational constraints such as driver shift patterns and specific job timing requirements. It features real-time, traffic-aware routing specifically designed for trucks, with the ability to dynamically replan routes based on current vehicle positions. The API intelligently matches specific job requirements with vehicle capabilities, such as refrigerated transport, while coordinating multiple vehicles to reduce overall travel time and fuel usage. Through its consideration of strict delivery windows and real-time traffic and roadway environment conditions, the API allows reliable delivery performance while maintaining the flexibility to adapt routes as conditions change.

Figure 1 shows how HERE Fleet Optimization addresses various fleet management problems.

Figure 1: Typical architecture utilizing HERE Fleet Optimization

**Emissions-Focused Routing based on Real-Time Intelligence**

HERE’s advanced routing system transforms traditional navigation by balancing environmental efficiency, cost, and speed. It employs robust algorithms that analyze multiple real-time variables to determine the most sustainable route for each journey. This intelligent approach considers that even minor variations in traffic patterns, vehicle specifications, or environmental conditions can impact fuel consumption and emissions.

The advanced routing tools continuously process real-time traffic data and provide updated routing information through HERE’s APIs. Fleet management systems implementing HERE’s routing capabilities can actively request new route calculations when needed, allowing them to respond to changes in road environmental conditions (such as changes in traffic regulations), accidents, construction work or other road conditions. By implementing these rerouting capabilities and invoking HERE’s APIs at appropriate intervals, systems can help vehicles avoid congestion and stop-and-go traffic. This approach reduces idle time and unnecessary acceleration, which are two major sources of excessive emissions.

Integrating HERE Real-Time Traffic and road alert features further enhances the intelligent routing system. These features provide quick updates about road conditions and potential hazards, enabling vehicles to maintain consistent speeds and avoid traffic bottlenecks. Different route options can be assessed for fuel efficiency and environmental effect via projected emissions comparison. The system evaluates predicted emissions for different routing options, comparing potential fuel consumption and environmental impact. While a suggested route may appear longer in distance, its forecasted emissions could be lower by avoiding predicted congestion zones, ultimately offering environmentally efficient path options. This comprehensive approach to routing combines real-time traffic data with vehicle-specific characteristics and environmental factors. By considering these multiple variables, businesses can achieve reductions in fuel consumption, idle time, and carbon emissions compared to traditional navigation approaches that focus solely on travel time or distance.

**Vehicle Telematics**

HERE’s routing system can integrate with vehicle telematics to monitor environmental performance metrics when [CAN bus data](https://en.wikipedia.org/wiki/CAN_bus) access is available. The system can analyze several key aspects for fleets with connected vehicle data, including actual fuel consumption data gathered from vehicles, patterns in driver behavior that impact efficiency, and opportunities to optimize routes and schedules.

This visibility enables fleet managers to make data-driven decisions about routing efficiency, driver coaching, and operational improvements. The insights help organizations measure and achieve their emissions reduction targets. However, monitoring actual fuel consumption relies specifically on vehicle data connectivity and access to CAN bus systems.

**Enhanced Visibility Solutions**

Last Mile delivery presents unique challenges in urban environments, where complicated traffic patterns and frequent stops significantly impact emissions. HERE’s shipment visibility combines data from multiple tracking sources – including IoT sensors and telematics systems – and enhances this information with precise location data. This gives customers a complete view of their shipments by integrating and enriching data from various tracking devices and platforms. This enhancement process maps positional information to precise locations, enabling real-time monitoring of delivery status against planned routes and schedules.

The platform evaluates whether shipments are running on time, behind schedule, or ahead of expectations, enabling fleet managers to monitor shipment progress comprehensively. Through real-time tracking of vehicle positions and delivery status, managers can assess schedule adherence and delivery performance while evaluating route compliance and timing variations. This visibility allows them to make dynamic adjustments as needed to optimize delivery efficiency across their operations.

This enhanced visibility allows operations teams to proactively address delays, optimize routing decisions, and remove unnecessary fuel consumption per package across the final delivery segment.

**Weather-Informed Decisions**

HERE Destination Weather is a dynamic (live) service delivering granular, up-to-the-minute, accurate and contextual local weather information to improve driver awareness and safety. The service provides current conditions, forecasts, severe weather alerts, and changing conditions along a journey. By integrating this detailed weather data into route planning, fleet managers can make smarter decisions, avoiding weather-related delays and increased fuel costs. This proactive approach helps optimize routes by considering current and predicted weather impacts on travel conditions.

**Measurable Customer Outcomes**

The implementation of HERE’s solutions has demonstrated significant environmental and business value, with the extent of benefits varying based on a company’s baseline. For organizations new to computer-based route optimization, these technologies can achieve up to 20% reduction in route times, fuel costs, and carbon footprint through efficient route planning and delivery optimization. Companies already using basic digitized routing solutions typically see gains of 5-8%, potentially reaching 10%, when upgrading to more advanced systems.

**Conclusion**

By combining geospatial data, advanced routing algorithms, and comprehensive fleet management capabilities, businesses can now achieve their environmental goals without compromising operational efficiency. As organizations worldwide face increasing pressure to reduce their environmental footprint, HERE’s technology stack, available through AWS Marketplace, offers a proven pathway to sustainable operations while maintaining competitive advantage in the global supply chain.

HERE Location Services and HERE Tour Planning are available as SaaS offerings in [AWS Marketplace](https://aws.amazon.com/marketplace/seller-profile?id=cc033bc0-fe05-4d79-ba58-9a132b1fe9d3) and have trial offers to help fleet customers test the solutions. Visit the [HERE Technologies](https://www.here.com/) website to learn more.