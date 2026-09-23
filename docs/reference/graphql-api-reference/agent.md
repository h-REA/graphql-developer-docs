# Agent

A person or group or organization with economic agency.

## Interface: `Agent`

| Field | Type | Description |
| ----- | ---- | ----------- |
| `id` | `ID!` | A unique identifier for the agent. |
| `revisionId` | `ID!` | The identifier of the last revision of this agent. |
| `name` | `String!` | An informal or formal textual identifier for an agent. Does not imply uniqueness. |
| `image` | `URI` | The uri to an image relevant to the agent, such as a logo, avatar, photo, etc. |
| `note` | `String` | A textual description or comment. |
| `relationships` | `AgentRelationshipConnection` | All relationships where this agent is either the subject or object. |
| `relationshipsAsSubject` | `AgentRelationshipConnection` | Relationships where this agent is the subject. |
| `relationshipsAsObject` | `AgentRelationshipConnection` | Relationships where this agent is the object. |
| `roles` | `[AgentRelationshipRole!]` | The relationship roles this agent has. |
| `commitments` | `CommitmentConnection` | All commitments where this agent is the provider or receiver. |
| `commitmentsAsProvider` | `CommitmentConnection` | Commitments where this agent is the provider. |
| `commitmentsAsReceiver` | `CommitmentConnection` | Commitments where this agent is the receiver. |
| `commitmentsInScope` | `CommitmentConnection` | Commitments that are in the scope of this agent. |
| `intents` | `IntentConnection` | All intents where this agent is the provider or receiver. |
| `intentsAsProvider` | `IntentConnection` | Intents where this agent is the provider. |
| `intentsAsReceiver` | `IntentConnection` | Intents where this agent is the receiver. |
| `intentsInScope` | `IntentConnection` | Intents that are in the scope of this agent. |
| `economicEvents` | `EconomicEventConnection` | All economic events where this agent is the provider or receiver. |
| `economicEventsAsProvider` | `EconomicEventConnection` | Economic events where this agent is the provider. |
| `economicEventsAsReceiver` | `EconomicEventConnection` | Economic events where this agent is the receiver. |
| `economicEventsInScope` | `EconomicEventConnection` | Economic events that are in the scope of this agent. |
| `inventoriedEconomicResources` | `EconomicResourceConnection` | Economic resources inventoried by this agent. |
| `plans` | `PlanConnection` | Plans created by this agent. |
| `processes` | `ProcessConnection` | Processes this agent is involved in. |
| `proposals` | `ProposalConnection` | All proposals involving this agent. |
| `proposalsInScope` | `ProposalConnection` | Proposals in the scope of this agent. |
| `proposalsTo` | `ProposalConnection` | Proposals made to this agent. |
| `revision` | `Agent` | Retrieves a specific revision of an agent. |
| `meta` | `RecordMeta!` | Metadata about the record. |

## Types implementing `Agent`

### `Person`

Represents a natural person. Inherits all fields from the `Agent` interface.

### `Organization`

Represents a formal or informal group, or legal organization. Inherits all fields from the `Agent` interface and has the following additional fields:

| Field | Type | Description |
| ----- | ---- | ----------- |
| `classifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |

## Queries

### `myAgent`
Loads details of the currently authenticated REA agent.

### `agent(id: ID!)`
Find an agent (person or organization) by their ID.

### `agents(first: Int, after: String, last: Int, before: String)`
Loads all agents publicly registered within this collaboration space.

### `organization(id: ID!)`
Find an organization (group) agent by its ID.

### `organizations(first: Int, after: String, last: Int, before: String)`
Loads all organizations publicly registered within this collaboration space.

### `person(id: ID!)`
Find a person by their ID.

### `people(first: Int, after: String, last: Int, before: String)`
Loads all people who have publicly registered with this collaboration space.

## Mutations

### `createPerson(person: AgentCreateParams!)`
Registers a new (human) person with the collaboration space.

### `updatePerson(person: AgentUpdateParams!)`
Updates profile details for a person.

### `deletePerson(revisionId: ID!)`
Erases the record of a person.

### `createOrganization(organization: OrganizationCreateParams!)`
Registers a new organization with the collaboration space.

### `updateOrganization(organization: OrganizationUpdateParams!)`
Updates profile details for an organization.

### `deleteOrganization(revisionId: ID!)`
Erases the record of an organization.

---

## Related Types

### Input: `AgentCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | An informal or formal textual identifier for an agent. |
| `image`| `URI` | A URI to an image for the agent. |
| `note` | `String` | A textual description or comment. |

### Input: `AgentUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the agent to update. |
| `name` | `String` | An informal or formal textual identifier for an agent. |
| `image`| `URI` | A URI to an image for the agent. |
| `note` | `String` | A textual description or comment. |

### Input: `OrganizationCreateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `name` | `String!` | An informal or formal textual identifier for the organization. |
| `image`| `URI` | A URI to an image for the organization. |
| `classifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |

### Input: `OrganizationUpdateParams`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `revisionId` | `ID!` | The revision ID of the organization to update. |
| `name` | `String` | An informal or formal textual identifier for the organization. |
| `image`| `URI` | A URI to an image for the organization. |
| `classifiedAs` | `[URI!]` | References concepts in a taxonomy for categorization. |
| `note` | `String` | A textual description or comment. |

### Response: `PersonResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `agent` | `Person!` | The person record that was created or updated. |

### Response: `OrganizationResponse`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `agent` | `Organization!` | The organization record that was created or updated. |

### Connection: `AgentConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[AgentEdge!]!` | A list of agent edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `AgentEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Agent!` | The agent record. |
| `cursor` | `String!` | A cursor for use in pagination. |

### Connection: `PersonConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[PersonEdge!]!` | A list of person edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `PersonEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Person!` | The person record. |
| `cursor` | `String!` | A cursor for use in pagination. |

### Connection: `OrganizationConnection`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `edges` | `[OrganizationEdge!]!` | A list of organization edges. |
| `pageInfo` | `PageInfo!` | Information to aid in pagination. |

### Edge: `OrganizationEdge`
| Field | Type | Description |
| ----- | ---- | ----------- |
| `node` | `Organization!` | The organization record. |
| `cursor` | `String!` | A cursor for use in pagination. |

