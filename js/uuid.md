# Uuid
```typescript
import { logger } from 'jege/server';
import os from 'os';

const log = logger('[uuid]');

const pid = getPid();
const mac = getMac();
let latestNow: number;

/**
 * pid range: < 99999 (255r, 36)
 * 4 digit
 */
function getPid(): string {
  if (process && process.pid) {
    return process.pid.toString(36)
      .padStart(4, '0');
  }
  log('getPid(): error getting pid');
  throw new Error('Error getting pid');
}

/**
 * trimmedString range: < 1999999999999 ('piscd0jj', 36)
 * 8 digits
 */
function getMac(): string {
  const networkInterfaces = os.networkInterfaces();
  let nonTrivialMac;

  Object.values(networkInterfaces)
    .find((networkInterface) => {
      for (let idx = 0; idx < networkInterface.length; idx += 1) {
        if (networkInterface[idx].mac && networkInterface[idx].mac !== '00:00:00:00:00:00') {
          nonTrivialMac = networkInterface[idx].mac;
          return true;
        }
      }
      return false;
    });

  if (nonTrivialMac) {
    const trimmedString = '1' + nonTrivialMac.replace(/\:/gi, '') // eslint-disable-line
      .replace(/\D/gi, 0);

    return parseInt(trimmedString, 10)
      .toString(36)
      .padStart(8, '0');
  }

  log('getMac(): error getting non trivial mac address');
  throw new Error('Error getting non trivial mac address');
}

function getTime(): string {
  const now = Date.now();
  const last = latestNow || now;
  const nextNow = now > last ? now : last + 1;
  latestNow = nextNow;

  const date = new Date(latestNow);
  const trimmedString = '1' + date.toISOString()
    .slice(2)
    .replace(/\D/gi, '');

  return parseInt(trimmedString, 10)
    .toString(36)
    .padStart(10, '0');
}

export default function uuid({
  prefix = '',
} = {}) {
  const time = getTime();
  return prefix + mac + pid + time;
}
```