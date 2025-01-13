# DataSelection

각 배열과 object를 활용하는 법을 배움. <br />
순서를 위해서 reverse()를 통해 순서를 맞춤.

마지막으로 수행되는 요소가 마지막으로 가야 한다면, 거꾸로 수행하는 것을 고려해볼 것!

```javascript
/**
 * @param {Array<{user: number, duration: number, equipment: Array<string>}>} sessions
 * @param {{user?: number, minDuration?: number, equipment?: Array<string>, merge?: boolean}} [options]
 * @return {Array}
 */
function setHasOverlap(setA, setB) {
  for (const val of Array.from(setA)) {
    if (setB.has(val)) {
      return true;
    }
  }

  return false;
}

export default function selectData(sessions, options = {}) {
  // 마지막으로 수행된 user가 마지막으로 가니까 reverse 함.
  const reversedSessions = sessions.slice().reverse();
  const sessionsForUser = new Map();
  const sessionsProcessed = [];

  reversedSessions.forEach((session) => {
    if (options.merge && sessionsForUser.has(session.user)) {
      const userSession = sessionsForUser.get(session.user);
      userSession.duration += session.duration;
      session.equipment.forEach((equipment) => {
        userSession.equipment.add(equipment);
      });
    } else {
      const clonedSessions = {
        ...session,
        equipment: new Set(session.equipment),
      };

      if (options.merge) {
        sessionsForUser.set(session.user, clonedSessions);
      }

      sessionsProcessed.push(clonedSessions);
    }
  });

  // 이제 진행된 순서대로 하면 되니까 다시 reverse 함.
  sessionsProcessed.reverse();

  const result = [];
  const optionEquipments = new Set(options.equipment);
  sessionsProcessed.forEach((session) => {
    if (options.user !== null && options.user !== session.user) return;
    if (
      optionEquipments.size > 0 &&
      !setHasOverlap(optionEquipments, session.equipment)
    )
      return;
    if (options.minDuration !== null && options.minDuration > session.duration)
      return;

    result.push({
      ...session,
      equipment: Array.from(session.equipment).sort(),
    });
  });

  return result;
}
```
